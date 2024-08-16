# E-Commerce-API

1. Add Swagger Dependencies
First, include the Swagger dependencies in your pom.xml file (for Maven) or build.gradle file (for Gradle).

Maven (pom.xml):
<dependencies>
    <!-- Other dependencies -->
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-boot-starter</artifactId>
        <version>3.0.0</version>
    </dependency>
</dependencies>

Gradle (build.gradle):
dependencies {
    // Other dependencies
    implementation 'io.springfox:springfox-boot-starter:3.0.0'
}
2. Create Swagger Configuration Class
Create a configuration class to set up Swagger for your project:
package com.example.ecommerce.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig {

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.example.ecommerce"))
                .paths(PathSelectors.any())
                .build();
    }
}

3. Run the Application
After setting up the configuration, run your Spring Boot application. Once the application is running, you can access the Swagger UI at:

URL: http://localhost:8080/swagger-ui/index.html
4. Customize API Documentation
You can further customize your Swagger documentation by adding annotations to your controllers and DTOs.

Example in a Controller:
package com.example.ecommerce.controller;

import com.example.ecommerce.dto.ProductDto;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/products")
@Api(value = "Product Management System")
public class ProductController {

    @ApiOperation(value = "Get a list of products")
    @GetMapping
    public ResponseEntity<List<ProductDto>> getAllProducts() {
        // Implementation
    }

    @ApiOperation(value = "Get a product by ID")
    @GetMapping("/{id}")
    public ResponseEntity<ProductDto> getProductById(@PathVariable Long id) {
        // Implementation
    }
}
5. Project Setup
Here’s how you can structure your project:

Directory Structure:
src
└── main
    ├── java
    │   └── com.example.ecommerce
    │       ├── controller
    │       ├── dto
    │       ├── model
    │       ├── repository
    │       ├── service
    │       ├── config
    │       └── EcommerceApplication.java
    └── resources
        ├── application.properties
        └── static
6. application.properties Configuration
Here’s an example of what your application.properties file might look like:
spring.datasource.url=jdbc:postgresql://localhost:5432/ecommerce
spring.datasource.username=your_db_username
spring.datasource.password=your_db_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# Swagger
springdoc.swagger-ui.path=/swagger-ui.html

# JWT Secret Key
jwt.secret=your_jwt_secret_key
7. Run and Verify
Run the Application: Make sure your database is set up and the application properties are correctly configured. Then, run the application.
Access Swagger UI: Open your browser and navigate to http://localhost:8080/swagger-ui/index.html to see the interactive API documentation.
Test API Endpoints: Use the Swagger UI to test the endpoints directly.
8. Generate API Documentation
Swagger UI itself serves as an interactive API documentation platform. However, you can also export the documentation as a JSON or YAML file if needed:

JSON: http://localhost:8080/v2/api-docs
YAML: http://localhost:8080/v3/api-docs.yaml
Conclusion
You now have a fully documented E-commerce API with a proper setup for your Spring Boot project. This setup ensures that your API is not only functional but also well-documented for easy use and testing by other developers or clients.
