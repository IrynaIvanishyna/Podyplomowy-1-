# Podyplomowy-1-
Projekt koncowy z wykorystaniem Selenium Webdriwer, na testowej stronie www.saucedemo.com

from selenium import webdriver
from selenium.webdriver.common.by import By as By
import unittest
from time import sleep

#Dane testowe
username = "standard_user"
password = "secret_sauce"


class WebsiteTests(unittest.TestCase):
    # Test nr 1, poprawne logowanie do strony saucedemo.com
    def test_login_correct(self):
        driver = webdriver.Chrome(executable_path="C:\\Users\\Irina\\Desktop\\chromedriver.exe")
        # Otworz stronę saucedemo.com
        driver.get("https://www.saucedemo.com")
        # Ustaw czas oczekiwania na element na 5 sekund
        driver.implicitly_wait(5)

        # Znajdz pole do wpisywania loginu
        login_box = driver.find_element(By.ID, "user-name")
        # Wpisz login
        login_box.send_keys(username)

        # Znajdż pole do wpisywania hasla
        password_box = driver.find_element(By.ID, "password")
        # Wpisz haslo
        password_box.send_keys(password)

        # Znajdż przycisk zalogowania
        login_button = driver.find_element(By.ID, "login-button")
        # Kliknij w przycisk
        login_button.click()

        # Znajdz tekst z tytulem strony
        title_element_text = driver.find_element(By.CLASS_NAME, "title")
        # Sprawdz czy tytul strony to "PRODUCTS"
        assert title_element_text.text == "PRODUCTS"

        # Test nr 2, niepoprawne logowanie do strony saucedemo.com
    def test_login_incorrect_password(self):
        driver = webdriver.Chrome(executable_path="C:\\Users\\Irina\\Desktop\\chromedriver.exe")
        # Otworz stronę saucedemo.com
        driver.get("https://www.saucedemo.com")
        # Ustaw czas oczekiwania na element na 5 sekund
        driver.implicitly_wait(5)

        # Znajdz pole do wpisywania loginu
        login_box = driver.find_element(By.ID, "user-name")
        # Wpisz login
        login_box.send_keys(username)

        # Znajdż pole do wpisywania hasla
        password_box = driver.find_element(By.ID, "password")
        # Kliknij w przycisk
        password_box.send_keys(username)

        # Znajdż przycisk zalogowania
        login_button = driver.find_element(By.ID, "login-button")
        # Kliknij w przycisk
        login_button.click()

        # Pobierz komunikat o błędzie
        error_message = driver.find_element(By.CLASS_NAME, "error-message-container")
        # Sprawdź czy komunikat posiada text:
        # "Epic sadface: Username and password do not match any user in this service"
        assert error_message.text == "Epic sadface: Username and password do not match any user in this service"

    # Test nr 3, dodawanie przedmotu do koszyka
    def test_add_to_basket(self):
        driver = webdriver.Chrome(executable_path="C:\\Users\\Irina\\Desktop\\chromedriver.exe")
        # Otworz stronę saucedemo.com
        driver.get("https://www.saucedemo.com")
        # Ustaw czas oczekiwania na element na 5 sekund
        driver.implicitly_wait(5)

        # Znajdz pole do wpisywania loginu
        login_box = driver.find_element(By.ID, "user-name")
        # Wpisz login
        login_box.send_keys(username)

        # Znajdż pole do wpisywania hasla
        password_box = driver.find_element(By.ID, "password")
        # Wpisz haslo
        password_box.send_keys(password)

        # Znajdż przycisk zalogowania
        login_button = driver.find_element(By.ID, "login-button")
        # Kliknij w przycisk
        login_button.click()

        # Znajdz tekst z tytulem strony
        title_element_text = driver.find_element(By.CLASS_NAME, "title")
        # Sprawdz czy tytul strony to "PRODUCTS"
        assert title_element_text.text == "PRODUCTS"

        # Znajdz przycisk dodania elementu do koszyka
        item_button = driver.find_element(By.ID, "add-to-cart-sauce-labs-backpack")
        # Kliknij w przycisk
        item_button.click()

        basket_button = driver.find_element(By.ID, "shopping_cart_container")
        basket_button.click()

        item_text = driver.find_element(By.ID, "item_4_title_link")
        assert item_text.text == "Sauce Labs Backpack"

        sleep(3)


if __name__ == "__main__":
    unittest.main(verbosity=3)



