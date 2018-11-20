1.使用@RequestBody注解时，有一个属性的变量名为

private Integer pAcId;
public Integer getPAcId() {
        return this.pAcId;
    }
public void setPAcId(Integer pAcId) {
        this.pAcId = pAcId;
    }
JSON转为对象时属性为null;


改为private Integer pacId;

public void setPacId(Integer pacId) {
        this.pacId = pacId;
    }
public Integer getPacId() {
        return this.pacId;
    }
    
    即可注入
    
    
    有时间需要研究一下源码
