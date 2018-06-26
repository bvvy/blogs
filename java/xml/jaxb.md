# jaxb完成对xml的解析

使用restTemplate 默认支持多种message converter
如果使用jaxb注意别和jackson xml冲突，默认优先使用后者

使用方式:
```
@XmlRootElemnt 来使用 
配置特殊信息再package-info 文件中配置
```