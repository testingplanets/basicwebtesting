import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.Test;

import java.time.Duration;

public class NEWTESTINGQAMANUALAUTOMATION {
    WebDriver driver;

        @Test
        public void loginTest() {
            //open browser
            WebDriverManager.chromedriver().setup();

            //WebDriver driver = new ChromeDriver();
            WebDriver driver = new FirefoxDriver();

            driver.manage().window().maximize();
            driver.get("https://katalon-demo-cura.herokuapp.com/");
            WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(30));

            //klik Make Appointment
            driver.findElement(By.xpath("//a[@class='btn btn-dark btn-lg']")).click();

            //input username dan password kemudian klik login
            wait.until((ExpectedConditions.visibilityOfElementLocated(By.xpath("//input[@name='username']"))));
            driver.findElement(By.name("username")).sendKeys("John Doe");
            driver.findElement(By.xpath("//input[@type='password']")).sendKeys("ThisIsNotAPassword");
            driver.findElement(By.xpath("//button[.='Login']")).click();

            //Verify berhasil login dengan text Make Appointment
            wait.until((ExpectedConditions.visibilityOfElementLocated(By.xpath("//h2[contains(.,'Make Appointment')]"))));
            String txtMakeAppointmentActual = driver.findElement(By.xpath("//h2[contains(.,'Make Appointment')]")).getText();
            String txtMakeAppointmentExpected = "Make Appointment";

            Assert.assertEquals(txtMakeAppointmentActual,txtMakeAppointmentExpected);
        }
}
