```java
import com.sun.net.httpserver.*;  
import org.json.JSONObject;  
  
import java.io.*;  
import java.net.InetSocketAddress;  
import java.nio.charset.StandardCharsets;  
  
public class SimpleHttpServer {  
  
    public static void main(String[] args) throws IOException {  
        int port = 8000;  
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);  
  
        // Обработчик для корневого пути "/"  
        server.createContext("/", new RootHandler());  
  
        // Обработчик для получения данных местоположения  
        server.createContext("/location", new LocationHandler());  
  
        server.setExecutor(null);  // Создает стандартный пул потоков  
        server.start();  
        System.out.println("Server is listening on port " + port);  
    }  
  
    // Обработчик для корневого пути  
    static class RootHandler implements HttpHandler {  
        @Override  
        public void handle(HttpExchange exchange) throws IOException {  
            String response = "Hello, World!";  
            exchange.sendResponseHeaders(200, response.length());  
            try (OutputStream os = exchange.getResponseBody()) {  
                os.write(response.getBytes());  
            }  
        }  
    }  
  
    // Обработчик для пути "/location"  
    static class LocationHandler implements HttpHandler {  
        @Override  
        public void handle(HttpExchange exchange) throws IOException {  
            if ("POST".equals(exchange.getRequestMethod())) {  
                // Логирование типа запроса и URI  
                System.out.println("Request Method: " + exchange.getRequestMethod());  
                System.out.println("Request URI: " + exchange.getRequestURI());  
  
                // Чтение данных из тела запроса  
                InputStream inputStream = exchange.getRequestBody();  
                String body = new String(inputStream.readAllBytes(), StandardCharsets.UTF_8);  
  
                // Логирование содержимого тела запроса  
                System.out.println("Received body: " + body);  
  
                try {  
                    // Парсинг JSON  
                    JSONObject jsonData = new JSONObject(body);  
                    double latitude = jsonData.getDouble("latitude");  
                    double longitude = jsonData.getDouble("longitude");  
  
                    // Логирование полученных данных о местоположении  
                    System.out.println("Получены координаты:");  
                    System.out.println("Широта: " + latitude);  
                    System.out.println("Долгота: " + longitude);  
  
                    // Формируем ответ  
                    String response = "Location received";  
                    exchange.sendResponseHeaders(200, response.length());  
                    try (OutputStream os = exchange.getResponseBody()) {  
                        os.write(response.getBytes());  
                    }  
  
                } catch (Exception e) {  
                    // Логирование ошибки при парсинге JSON  
                    System.out.println("Ошибка при парсинге JSON: " + e.getMessage());  
  
                    // Отправка ошибки 400 Bad Request в случае некорректных данных  
                    String errorResponse = "Invalid JSON format";  
                    exchange.sendResponseHeaders(400, errorResponse.length());  
                    try (OutputStream os = exchange.getResponseBody()) {  
                        os.write(errorResponse.getBytes());  
                    }  
                }  
            } else {  
                // Отправляем ответ 405, если метод запроса не POST  
                exchange.sendResponseHeaders(405, -1);  
                System.out.println("Received unsupported HTTP method: " + exchange.getRequestMethod());  
            }  
        }  
    }  
}
```
Проверен: **postman**
POST http://localhost:8000/location
BODY  RAW
```
{
	"latitude": 55.7558,
	"longitude": 37.6173
}
```

POM.XML  ==(Добавить)==
```java
<dependencies>  
    <!-- Зависимость для работы с JSON -->  
    <dependency>  
        <groupId>org.json</groupId>  
        <artifactId>json</artifactId>  
        <version>20190722</version>  
    </dependency>  
</dependencies>
```