from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import time
import tkinter as tk

options = Options();
# prevent the browser from closing
options.add_experimental_option("detach", True)
# create a driver instance
driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
        
def popup_window(title, message):
    window = tk.Tk()
    window.title(title)
    label = tk.Label(window, text=message)
    label.pack()
    button = tk.Button(window, text="OK", command=window.destroy)
    button.pack()
    window.mainloop()

def getIntoLoginPage():
    # Get to list of examinees
    ##### - Transition between pages
    try:
        # navigate to Psifas
        driver.get("https://amanathome.co.il/Reports/ViewReport.aspx?q95hUPVIPLvbnJnCwzfDaNDF4Cuo+Qgrnu2c57eF448ROYvBRujxAvFMuZWQE94daqzEiGzVXLVT5E/z3Tup4ExmtHp9sdl2u5B2yobmgCgGxR2lBrUcKRT9kW2ILgxaEdQDxLyT5VmpxHzJgj4Yng==PPP")
        username_input = driver.find_element(By.ID, "Login1_UserName")
        password_input = driver.find_element(By.ID, "Login1_Password")

        username_input.send_keys("oz")
        password_input.send_keys("Oz@haman2022")
        username_input.send_keys(Keys.RETURN)

#####

        list_of_examinees_link = driver.find_element(By.ID, 'ctl00_SideMenuControl1_HyperLink1')
        list_of_examinees_link.click()

#####

        starting_date_input = driver.find_element(By.ID, "ctl00_cphContentPane_ctl00_txtFrom")
        final_date_input = driver.find_element(By.ID, "ctl00_cphContentPane_ctl00_txtTo")
        produce_report_button = driver.find_element(By.ID, "ctl00_cphContentPane_ctl00_btnRunReport")

        ''' 
        # TODO: make a gui for date inputs      
        print("Enter a date range of examinees")
        starting_date_text = input("starting date: ")
        final_date_text = input("final date: ")
        starting_date_input.send_keys(starting_date_text)
        final_date_input.send_keys(final_date_text)
        ''' 

        starting_date_input.send_keys("01/01/2023")
        final_date_input.send_keys("01/17/2023")
        original_window = driver.current_window_handle
        produce_report_button.click()

#####

        # Switch to the new window
        for handle in driver.window_handles:
            if handle != original_window:
                driver.close()
                driver.switch_to.window(handle)

        # Get the URL of the new window
        new_window_url = driver.current_url

        driver.get(new_window_url)
        main_div = driver.find_element(By.TAG_NAME, "tbody")
        main_div_dom = main_div.get_attribute("outerHTML")
        # popup_window(str(new_window_url), str(new_window_url))
        # main_div = driver.find_element(By.ID, "wrap")

        popup_window(str(main_div), str(main_div))

    except Exception as ex:
        if ex:
            print("hi: \n", ex) 

getIntoLoginPage()