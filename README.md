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

### WebSecurityConfigurerAdapter
Provides a convenient base class for creating a WebSecurityConfigurer instance. The implementation allows customization by overriding methods.

#### configure(HttpSecurity http)
It defines which URL paths should be secured and which should not.

The following code block is required.
```kotlin
http
    ?.authorizeRequests()
    ?.anyRequest()
    ?.authenticated()
```

- `?` matches one character
- `*` matches zero or more characters
- `**` matches zero or more 'directories' in a path
- `{spring:[a-z]+}` matches the regexp `[a-z]+` as a path variable named "spring"


The following code block is permitting to access the path defined with Ant-style pattern.
`"\"` and `"\home"` is permitted to access without authentication.
```kotlin
http?.authorizeRequests()
    ?.antMatchers("/", "/home")?.permitAll()
```

The following code block is Forms Authentication.
```kotlin
http?.formLogin()
```

You can define a custom Form Login page as following
```kotlin
http?.formLogin()?.loginPage("/login")
```

The following code block is providing custom login view.
```kotlin
http?.formLogin()
```

### UserDetailsService
`userDetailsService()` method sets up an in-memory user store with a single user. 
- **Username**: `user`
- **Password**: `password`
- **Role**: `USER`

```kotlin
val user: UserDetails = User.withDefaultPasswordEncoder()
        .username("user")
        .password("password")
        .roles("USER")
        .build()
return InMemoryUserDetailsManager(user)
```

### Custom Login View
- `src/main/resources/templates/login.html`

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="https://www.thymeleaf.org"
      xmlns:sec="https://www.thymeleaf.org/thymeleaf-extras-springsecurity3">
    <head>
        <title>Spring Security Example </title>
    </head>
    <body>
        <div th:if="${param.error}">
            Invalid username and password.
        </div>
        <div th:if="${param.logout}">
            You have been logged out.
        </div>
        <form th:action="@{/login}" method="post">
            <div><label> User Name : <input type="text" name="username"/> </label></div>
            <div><label> Password: <input type="password" name="password"/> </label></div>
            <div><input type="submit" value="Sign In"/></div>
        </form>
    </body>
</html>
```

The thymeleaf template posts `username` and `password` to `/login`.
```html
<form th:action="@{/login}" method="post">
```

If you fail to login, Spring Security redirects to `/login?error`. You can retrieve `error` parameter by EL `${param.error}`.
```html
<div th:if="${param.error}">
```

When you logout, Spring Security redirects to `/login?logout`.
```html
<div th:if="${param.logout}">
```

If you want to change logout url, you can modify definition same Form Login.
```kotlin
logout()?.logoutSuccessUrl("/logout")?.permitAll()
```

### Display Username
- You can display login username by `HttpServletRequest#getRemoteUser()`
- You can logout when you access to `/logout`
```html
<h1 th:inline="text">Hello [[${#httpServletRequest.remoteUser}]]!</h1>
<form th:action="@{/logout}" method="post">
    <input type="submit" value="Sign Out"/>
</form>
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
