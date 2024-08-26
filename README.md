# Robot-to-receive-loans
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select
import time
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.by import By
from selenium.webdriver.support import expected_conditions as EC


# تنظیمات مرورگر
driver = webdriver.Edge()  # از مرورگر Edge استفاده کنید
driver.get("https://ve.cbi.ir/TasRequest.aspx")
time.sleep(40)  # تاخیر زمانی برای بارگذاری صفحه

# وارد کردن شماره ملی
national_id_input = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_tbIDNo"]')
national_id_input.send_keys("1990000240")

# انتخاب روز  تولد
day_dropdown = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_ddlBrDay"]')
day_select = Select(day_dropdown)
day_select.select_by_value('10')  #    تاریخ دهم روز تولد

#  ماه

WebDriverWait(driver, 20).until(EC.element_to_be_clickable((By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_ddlBrMonth"]'))).send_keys('فروردین')

# سال تولد

year_input = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_tbBrYear"]')
year_input.send_keys('1377')

# انتخاب روز  ازدواج
day_dropdown = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_ddlMarryDay"]')
day_select = Select(day_dropdown)
day_select.select_by_value('18')  #    تاریخ ازدواج  روز دهم

# انتخاب ماه ازدواج
WebDriverWait(driver, 20).until(EC.element_to_be_clickable((By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_ddlMarryMonth"]'))).send_keys('آذز')

# # انتخاب سال ازدواج (اگر نیاز باشد)
year_input = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_tbMarrYear"]')
year_input.send_keys('1400')


# شماره تلفن همراه :

national_id_input = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_tbMobileNo"]')
national_id_input.send_keys('09106627998')

# لطفا گزینه درست
# را انتخاب نمایید :

national_id_input = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_rbtnMarrKind1"]').click()
#  استان محل سکونت: 
WebDriverWait(driver, 20).until(EC.element_to_be_clickable((By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_ddlState"]'))).send_keys('تهران')


# کپچا 
import cv2
import pytesseract
import requests

# مسیر آدرس تصویر کپچا
captcha_url = 'https://ve.cbi.ir/TasRequest.aspx'

# درخواست GET برای دریافت تصویر کپچا
response = requests.get(captcha_url)

# ذخیره تصویر کپچا در فایل (مسیر دلخواه)
save_path = 'C:/Users/click/Desktop/python15/Data/captcha_result.png'
with open(save_path, 'wb') as f:
    f.write(response.content)

# تصویر را به صورت خاکستری بخوانید
img = cv2.imread(save_path, 0)
# تشخیص متن فارسی از تصویر
text = pytesseract.image_to_string(img, lang='fas')  # 'fas' برای زبان فارسی

# تشخیص عبارت‌های ریاضی از متن استخراج شده
# national_id_input = driver.find_element(By.XPATH, '//*[@id="ctl00_ContentPlaceHolder1_tbCaptcha"]').click()
