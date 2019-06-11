###enum 类型 返回JSON数据时返回的时枚举名称  如下只返回 "INVOICE"  字符串


解决：@JsonFormat(shape = JsonFormat.Shape.OBJECT) 在类上加入该注解 可返回期待的结果
maven:
    <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-annotations</artifactId>
          <version>2.9.8</version>
      </dependency>

public enum SupportEnum {
    INVOICE("本店支持开发票",
            "999999",
            "票",
            "开发票");
            }
            
            
            
result:
          {
                "description":"本店支持开发票",
                "icon_color":"999999",
                "icon_name":"票",
                "name":"开发票"
            }
