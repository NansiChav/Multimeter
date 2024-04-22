#include <LiquidCrystal.h>
#include <DHT.h>

// Define the pin for the DHT sensor
#define DHT11_PIN 7

// Define pins for the LCD display
const int rs = 4, en = 6, d4 = 10, d5 = 11, d6 = 12, d7 = 13;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

// Define the pin for the relay
const int relay = 2;

// Create a DHT object
DHT dht(DHT11_PIN, DHT11);

// Setup function, runs once when the microcontroller starts
void setup() {
  // Initialize the LCD display
  lcd.begin(16, 2);

  // Initialize the DHT sensor
  dht.begin();

  // Set the relay pin as an output
  pinMode(relay, OUTPUT);
}

// Loop function, runs repeatedly after setup
void loop() {
  // Call the LCD_Write function
  LCD_Write();
}

// Function to write data to the LCD display
void LCD_Write() {
  // Read temperature from the DHT sensor
  float temperature = dht.readTemperature();

  // Read air humidity from the DHT sensor
  float airHumidity = dht.readHumidity();

  // Adjust air humidity value
  airHumidity -= 100;
  airHumidity *= -1;

  // Read soil humidity using the checkSoil function
  float soilHumidity = checkSoil();

  // Display temperature and soil humidity on the first line of the LCD
  lcd.setCursor(0, 0);
  lcd.print("T:");
  lcd.print(temperature);
  lcd.print((char)223);
  lcd.print("C ");
  lcd.print("SH:");
  lcd.print((int)soilHumidity);
  lcd.print("%");

  // Display air humidity on the second line of the LCD
  lcd.setCursor(0, 1);
  lcd.print("Air Humdt:");
  lcd.print(airHumidity);
  lcd.print("% ");
}

// Function to check soil moisture
int checkSoil() {
  // Variable to store soil moisture level
  int soilMoisture = 0;

  // Read the analog value from the soil moisture sensor and convert it to a percentage
  soilMoisture = map(analogRead(A0), 0, 1024, 0, 100);

  // Adjust soil moisture value
  soilMoisture = (soilMoisture - 100) * -1;

  // Return the soil moisture level as a percentage
  return soilMoisture;
}
