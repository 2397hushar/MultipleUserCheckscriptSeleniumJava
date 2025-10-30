# MultipleUserCheckscriptSeleniumJava

package tests;

import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.*;
import io.github.bonigarcia.wdm.WebDriverManager;
import java.time.Duration;
import java.util.*;
import java.util.NoSuchElementException;

public class Hello {
    public static void main(String[] args) throws InterruptedException {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.manage().window().maximize();

        String baseUrl = "https://preprod-hubbleorion.hubblehox.com/";

        Map<String, String> users = new LinkedHashMap<>();
        users.put("khanmasroor51@gmail.com", "Khan@123");
        users.put("khanmasroor51@gmail.com", "Khan@123");
        users.put("saujain87@gmail.com", "Sauj@123");
        users.put("charitra@vestalrubber.com", "Char@123");
        users.put("kuber.shinde442@gmail.com", "Kube@123");
        users.put("ke2success@yahoo.co.in", "Ke2s@123");
        users.put("sks3286@gmail.com", "Sks3@123");
        users.put("patkarninad@gmail.com", "Patk@123");
        users.put("graminartse@gmail.com", "Gram@123");
        users.put("mr.sanju.k@gmail.com", "Mr.s@123");
        users.put("rishikalra15089@gmail.com", "Rish@123");
        users.put("sachinbd009@gmail.com", "Sach@123");
        users.put("rishit.shah25@gmail.com", "Rish@123");
        users.put("someshsjce@gmail.com", "Some@123");
        users.put("senra1994@gmail.com", "Senr@123");
        users.put("ivanofucci@gmail.com", "Ivan@123");
        users.put("sanjana.tambe1997@gmail.com", "Sanj@123");
        users.put("bhattbhadrik@gmail.com", "Bhat@123");
        users.put("vishalagarwal562@gmail.com", "Vish@123");
        users.put("gauravchoudhary28@gmail.com", "Gaur@123");
        users.put("shwetapandit7@gmail.com", "Shwe@123");
        users.put("akshaymalde129@gmail.com", "Aksh@123");
        users.put("shriyalveneerse@gmail.com", "Shri@123");
        users.put("zikrunkhan78@gmail.com", "Zikr@123");
        users.put("gada.jyoti@gmail.com", "Gada@123");
        users.put("jainruby27390@gmail.com", "Jain@123");
        users.put("bhargavi_bhatt@gmail.com", "Bhar@123");
        users.put("gina.a.john@gmail.com", "Gina@123");
        users.put("samidhaprabhu@yahoo.com", "Sami@123");
        users.put("piyush.mar@gmail.com", "Piyu@123");
        users.put("purvinandu.pn@gmail.com", "Purv@123");
        users.put("chandanasomesh@gmail.com", "Chan@123");
        users.put("arti.dogra2622@gmail.com", "Arti@123");
        users.put("amardeepfornet@yahoo.co.in", "Amar@123");
        users.put("bijal.rana@gmail.com", "Bija@123");
        users.put("dvsingh285@gmail.com", "Dvsi@123");
        users.put("anugill03@gmail.com", "Anug@123");
        users.put("mitums@gmail.com", "Mitu@123");
        users.put("580agarwal@gmail.com", "Alka@123");
        users.put("poojapatil25031998@gmail.com", "Pooj@123");
        users.put("jain.mona07@gmail.com", "Jain@123");
        users.put("anki2710@gmail.com", "Anki@123");
        users.put("102341@vgos.org", "Vxud@123");
        users.put("ksbmatharu@gmail.com", "Ksbm@123");
        users.put("102342@vgos.org", "Iuhr@123");
        users.put("abhay.6581@gamil.com", "Abha@123");
        users.put("anusha.smiley93@gmail.com", "Anus@123");
        users.put("kushal.dinesh@gmail.com", "Kush@123");
        users.put("sharmamadhuri2014@gmail.com", "Shar@123");
        users.put("mathurruchitam@gmail.com", "Math@123");
        users.put("shahinkhan.hsc7@gmail.com", "Shah@123");
        users.put("karthikkumarmrf.@gmail.com", "NULL");
        users.put("nareshkalra42@yahoo.com", "Nare@123");
        users.put("arbind.sinha@hcltech.com", "Arbi@123");
        users.put("vkshvrm6@gmail.com", "Vksh@123");
        users.put("gayatri.agrawal30@gmail.com", "Gaya@123");
        for (Map.Entry<String, String> entry : users.entrySet()) {
            String email = entry.getKey();
            String password = entry.getValue();

            driver.get(baseUrl);
            WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(15));

            try {
                // Wait for the Keycloak SSO page to load
                wait.until(ExpectedConditions.or(
                    ExpectedConditions.visibilityOfElementLocated(By.id("username")),
                    ExpectedConditions.visibilityOfElementLocated(By.id("email"))
                ));

                // Handle dynamic ID (username or email)
                WebElement emailField;
                try {
                    emailField = driver.findElement(By.id("username"));
                } catch (NoSuchElementException e) {
                    emailField = driver.findElement(By.id("email"));
                }

                WebElement passwordField = driver.findElement(By.id("password"));

                // Try normal sendKeys first
                try {
                    emailField.click();
                    emailField.clear();
                    emailField.sendKeys(email);
                } catch (Exception e) {
                    // If normal typing fails, use JS executor
                    ((JavascriptExecutor) driver).executeScript("arguments[0].value='" + email + "';", emailField);
                }

                try {
                    passwordField.click();
                    passwordField.clear();
                    passwordField.sendKeys(password);
                } catch (Exception e) {
                    ((JavascriptExecutor) driver).executeScript("arguments[0].value='" + password + "';", passwordField);
                }

                // Wait and click login button
                WebElement loginButton = wait.until(ExpectedConditions.elementToBeClickable(By.id("kc-login")));
                ((JavascriptExecutor) driver).executeScript("arguments[0].click();", loginButton);

                // Wait after login for dashboard or error
                Thread.sleep(4000);

                boolean loginSuccess;
                try {
                    driver.findElement(By.xpath("//*[contains(text(),'Dashboard') or contains(text(),'Home')]"));
                    loginSuccess = true;
                } catch (Exception e) {
                    loginSuccess = false;
                }

                if (loginSuccess) {
                    System.out.println("✅ PASS: " + email + " logged in successfully.");
                } else {
                    System.out.println("❌ FAIL: " + email + " login failed.");
                }

            } catch (Exception e) {
                System.out.println("⚠️ ERROR while testing user " + email + ": " + e.getMessage());
            }
        }

        driver.quit();
    }
}
