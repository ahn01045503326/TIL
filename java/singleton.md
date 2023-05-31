# singoleton

---

````
public class CompanyInfo 
{
    private static CompanyInfo innstance;
 
    private String companyName;
    private String companyAddr;
    
    
    private CompanyInfo()
    {
    }
    
    public static CompanyInfo getInstance()
    {
        if (innstance == null)
        {
            synchronized(CompanyInfo.class)
            {
                innstance = new CompanyInfo();
            }
        }
        
        return innstance;
    }
    
    
    // getter, setter 
    public String getCompanyName() {
        return companyName;
    }
 
    public void setCompanyName(String companyName) {
        this.companyName = companyName;
    }
 
    public String getCompanyAddr() {
        return companyAddr;
    }
 
    public void setCompanyAddr(String companyAddr) {
        this.companyAddr = companyAddr;
    }    
}
````

````
CompanyInfo companyInfo = CompanyInfo.getInstance();
````

Singleton 클래스가 하나의 인스턴스만 유지되도록 구현됩니다. 

싱글톤 패턴에서는 클래스의 생성자가 private으로 선언되므로 다른 클래스에서는 이 클래스의 인스턴스를 생성할 수 없습니다.

getInstance() 메소드를 호출하면 Singleton 클래스의 인스턴스가 반환됩니다. 

이 메소드는 먼저 instance 변수를 확인하여 null인 경우에만 인스턴스를 생성합니다. 
