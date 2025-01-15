from appium import webdriver
from selenium.webdriver.common.by import By
import time

# คำสั่งในการเชื่อมต่อกับ Appium
desired_caps = {
    'platformName': 'Android',
    'deviceName': 'Android Emulator',  # เปลี่ยนเป็นชื่ออุปกรณ์ของคุณ
    'browserName': 'Chrome',
    'automationName': 'UiAutomator2',
}

# เชื่อมต่อกับ Appium และสร้าง driver
try:
    driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
except Exception as e:
    print(f"Error connecting to Appium server: {e}")
    exit(1)  # ออกจากโปรแกรมหากไม่สามารถเชื่อมต่อกับ Appium

# เปิดเว็บไซต์
driver.get("https://play.hubhengjing888.xyz/")

# รอให้เว็บไซต์โหลด
time.sleep(3)

# ตรวจสอบการเข้าสู่ระบบ
try:
    # กรอกข้อมูลยูสเซอร์
    user_input = driver.find_element(By.XPATH, "//input[@name='username']")  # ใช้ XPATH ของ input ที่ใช้กรอกยูสเซอร์
    user_input.send_keys("hbhj092667copy")

    # กรอกรหัสผ่าน
    password_input = driver.find_element(By.XPATH, "//input[@name='password']")  # ใช้ XPATH ของ input ที่ใช้กรอกรหัสผ่าน
    password_input.send_keys("123456Bb")

    # กดปุ่มเข้าสู่ระบบ https://play.hubhengjing888.xyz/abatech# ใช้ XPATH ของปุ่มเข้าสู่ระบบ
    login_button.click()

    # รอให้การเข้าสู่ระบบเสร็จสมบูรณ์
    time.sleep(5)

    # ตรวจสอบ Rank และเครดิตคงเหลือ
    # หาข้อมูล Rank
    rank_element = driver.find_element(By.XPATH, "//div[@id='currentRanking']")  # ปรับ XPATH ให้ตรงกับที่ของ Rank
    print(f"Current Rank: {rank_element.text}")

    # ข้อมูลเครดิตคงเหลือ coin
    coin_element = driver.find_element(By.XPATH, "//div[@id='coin']")  # ปรับ XPATH ให้ตรงกับที่ของ coin
    print(f"Coin balance: {coin_element.text}")

    # ข้อมูลแต้ม diamond
    diamond_element = driver.find_element(By.XPATH, "//div[@id='diamond']")  # ปรับ XPATH ให้ตรงกับที่ของ diamond
    print(f"Diamond points: {diamond_element.text}")

    # หาข้อมูลฝาก coin
    deposit_coin_element = driver.find_element(By.XPATH, "//div[@id='depositCoin']")  # ปรับ XPATH ให้ตรงกับที่ของ deposit coin
    print(f"Deposit Coin: {deposit_coin_element.text}")
except Exception as e:
    print(f"Error during interaction: {e}")
finally:
    # ปิดเบราว์เซอร์
    driver.quit()
