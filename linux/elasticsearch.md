### 安装 elasticsearch 6.0


#### 1. 下载安装
    
        
下载rpm文件
    
    wget http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm?AuthParam=1512182326_f431dbb4f9f42d2015588ce8e3ed8d90
安装
    rpm -i jdk-8u151-linux-x64.rpm?AuthParam=1512182326_f431dbb4f9f42d2015588ce8e3ed8d90 
    
#### 2. 修改配置

  创建一个用户 elasticsearch 设置密码 sanduspace1202 并给与权限
      
      useradd elasticsearch
      passwd sanduspace1202
      chown -R elasticsearch /usr/local/elasticsearch
 
  修改 vim config/elasticsearch.yml

    network.host: 0.0.0.0
  
  修改 vim /etc/sysctl.conf 
 
    vm.max_map_count=655360
    
  修改添加 vim /etc/security/limits.conf
  
    elasticseach  hard nofile 65536
    elasticseach  soft nofile 65536
    
  执行命令 查看修改
    
    sysctl -p
    ulimit -Hn

#### 3 安装ik分词器

    elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.0.0/elasticsearch-analysis-ik-6.0.0.zip

#### 4. 运行elasticsearch: 
    
    bin/elasticsearch -d


### 安装 配置 logstash

#### 下载logstash

#### 安装 logstash jdbc input 完成数据的导入

#### logstash 导入脚本 product_recommend.conf
    
    input {
      stdin {
      }
      jdbc {
      # mysql jdbc connection string to our backup databse
      jdbc_connection_string => "jdbc:mysql://192.168.1.107:3306/app_online_30"
      # the user we wish to excute our statement as
      jdbc_user => "root"
      jdbc_password => "Sandu_218root"
      # 制定mysql驱动位置
      jdbc_driver_library => "/usr/share/logstash/mysql-connector-java-5.1.44.jar"
      # the name of the driver class for mysql
      jdbc_driver_class => "com.mysql.jdbc.Driver"
      jdbc_paging_enabled => "true"
      # 表示每查到50000条记录插入一次索引
      jdbc_page_size => "50000"
    #以下对应着要执行的sql的绝对路径。
      statement_filepath => "/usr/share/logstash/bin/product_recommend.sql"
    #定时字段 各字段含义（由左至右）分、时
    #、天、月、年，全部为*默认含义为每分钟都更新 如果每五分钟执行 */5 * * * * 不写表示只执行一次
    #  schedule => "* * * * *"
    #设定ES索引类型
    #  type => "bd_dev_dlq"
      }
    }
    
    #filter {
    #  json {
    #  source => "message"
    #  remove_field => ["message"]
    #  }
    #}
    
    output {
      elasticsearch {
    #ESIP地址与端口
      hosts => "http://192.168.1.122:9200/"
    #ES索引名称（自己定义的）
      index => "product_recommend"
    #自增ID编号
      document_id => "%{product_id}"
      }
      stdout {
    #以JSON格式输出
      codec => json_lines
      }
    }

sql 文件 product_recommend.sql
    
    SELECT
      bp.id           AS product_id,
      bp.product_name AS product_name,
      bp.color_id     AS color_id,
      bp.product_code AS product_code,
      bp.style_id     AS style_id,
      ps.style_name   AS style_name,
      bb.id           AS brand_id,
      bb.brand_name   AS brand_name,
      bc.id           AS company_id,
      bc.company_name AS company_name,
      bp.putaway_state as state,
      bp.sale_price as price,
      bp.product_spec as product_spec,
      bp.house_type_values as house_type_value,
      bp.colors_long_code as colors_long_code,
      bp.measure_code as measure_code,
      bp.decoration_id as decoration_id
    FROM base_product bp LEFT JOIN product_style ps ON ps.id = bp.style_id
      LEFT JOIN base_brand bb ON bb.id = bp.brand_id
      LEFT JOIN base_company bc ON bc.id = bb.company_id

#### 启动logstash 
    
    ./logstash -f product_recommend.conf