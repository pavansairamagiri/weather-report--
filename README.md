package javanew.PAVAN;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class WeatherApp {

    private static final String API_URL = "https://samples.openweathermap.org/data/2.5/forecast/hourly?q=London,us&appid=b6907d289e10d714a6e88b30761fae22";

    public static void main(String[] args) {
        try {
            String weatherData = getWeatherData(API_URL);
            if (weatherData != null) {
                while (true) {
                    displayMenu();
                    int choice = getUserChoice();
                    switch (choice) {
                        case 1:
                            printWeather(weatherData);
                            break;
                        case 2:
                            printWindSpeed(weatherData);
                            break;
                        case 3:
                            printPressure(weatherData);
                            break;
                        case 0:
                            System.out.println("Exiting the program.");
                            return;
                        default:
                            System.out.println("Invalid choice. Please try again.");
                            break;
                    }
                }
            }
        } catch (IOException e) {
            System.out.println("Failed to retrieve weather data.");
        }
    }

    private static String getWeatherData(String apiUrl) throws IOException {
        StringBuilder result = new StringBuilder();
        URL url = new URL(apiUrl);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET");

        try (BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream()))) {
            String line;
            while ((line = reader.readLine()) != null) {
                result.append(line);
            }
        }

        return result.toString();
    }

    private static void displayMenu() {
        System.out.println("\nOptions:");
        System.out.println("1. Get weather");
        System.out.println("2. Get Wind Speed");
        System.out.println("3. Get Pressure");
        System.out.println("0. Exit");
    }

    private static int getUserChoice() throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        System.out.print("Enter your choice: ");
        String input = reader.readLine();
        try {
            return Integer.parseInt(input);
        } catch (NumberFormatException e) {
            return -1;
        }
    }

    private static void printWeather(String weatherData) {
        System.out.println("Printing weather information...");
    }

    private static void printWindSpeed(String weatherData) {
        System.out.println("Printing wind speed information...");
    }

    private static void printPressure(String weatherData) {
        System.out.println("Printing pressure information...");
    }
}
