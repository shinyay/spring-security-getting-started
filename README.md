# Spring Security Getting Started

Getting Started with Simple Web application protected by Spring Security

## Description
### Dependency
- spring-boot-starter-security
- spring-boot-starter-web
- spring-boot-starter-thymeleaf

### EnableWebSecurity
`AnnotationConfigWebApplicationContext` reads `@EnableWebSecurity` annotated class.
Generally `@EnableWebSecurity` annotated class extends `WebSecurityConfigurerAdapter`
The application demands *User* and *Password* even if you don't put `@EnableWebSecurity` class. Therefore you should override the security action or remove Security dependency.

### WebMvcConfigurer
Defines callback methods to customize the Java-based configuration for Spring MVC

#### addViewControllers(ViewControllerRegistry registry)
Configure simple automated controllers pre-configured with the response status code and/or a view to render the response body.

```kotlin
override fun addViewControllers(registry: ViewControllerRegistry) {
    registry.addViewController("/home").setViewName("home")
}
```

## Demo

## Features

- feature:1
- feature:2

## Requirement

## Usage

## Installation

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/34c6fdd50d54aa8e23560c296424aeb61599aa71/LICENSE)

## Author

[shinyay](https://github.com/shinyay)
