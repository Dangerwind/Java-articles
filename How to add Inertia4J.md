**Подключение библиотеки Inertia4j в проект на Spring Boot**

Чтобы использовать Inertia.js в вашем Spring Boot-приложении, достаточно подключить библиотеку Inertia4j. Ниже приведены способы установки для Gradle и Maven.

**Gradle с libs.version.toml**

Если вы используете каталог версий (libs.versions.toml), подключение выглядит следующим образом:

build.gradle.kts:
```java
dependencies {
// остальные зависимости проекта...
    implementation(libs.inertia4jSpring)
}
```

gradle/libs.version.toml:
```
[versions]
# версии остальных библиотек проекта...
inertia4j-spring = "1.0.4"

[libraries]
# остальные зависимости проекта...
inertia4jSpring = { module = "io.github.inertia4j:inertia4j-spring", version.ref = "inertia4j-spring" }
```

**Gradle без libs.versions.toml**
   
Если вы не используете каталог версий, просто добавьте зависимость напрямую в build.gradle.kts:

```
dependencies {
// остальные зависимости проекта...
    implementation("io.github.inertia4j:inertia4j-spring:1.0.4")
}
```

Или для build.gradle:

```
// остальные зависимости проекта...
dependencies {
    implementation 'io.github.inertia4j:inertia4j-spring:1.0.4'
}
```


**Maven**
   
Если ваш проект построен на Maven, добавьте зависимость в pom.xml:

```
<dependency>
<!-- остальные зависимости проекта -->
    <groupId>io.github.inertia4j</groupId>
    <artifactId>inertia4j-spring</artifactId>
    <version>1.0.4</version>
</dependency>
```

Версия inertia4j 1.0.4 выпущена 26 мая 2025 года. 
   
---
   
**Использование Inertia в контроллере**

Импортируем и внедряем бин.
```java
import io.github.inertia4j.spring.Inertia;
// прочие import по вашему проекту

@RequiredArgsConstructor
// ваши анотации, к примеру @RestController
public class ExampleController {

    private final Inertia inertia;
// ваш код ...    
```
Можно использовать класический вариант `@Autowired` перед `private final Inertia inertia;` если не хотите использовать Lombok (@RequiredArgsConstructor).

**Формирования ответа**

**Метод render(String page, Map<String, Object> props)**

Метод render формирует ответ для Inertia.js на фронтенд-страницу. Он используется, когда клиент делает обычный GET-запрос и ожидает увидеть страницу, наполненную данными.

Параметр page: строка, указывающая имя страницы, которая отобразится на фронте (например, компонент Vue/React с тем же именем).

Параметр props: карта данных (пропсы), которые автоматически сериализуются и передаются на компонент на фронтенде. 
`Map<String, Object> props = тут ваши данные которые хотите передать`
   
Пример: `return inertia.render("ProfilePage", props);`
    
**Метод redirect(String page)**
Метод redirect создаёт инерциальный редирект — это не обычный HTTP-редирект (302/303), а внутренний механизм для навигации по страницам без полной перезагрузки браузера.

Обычно вызывается после POST/PUT/DELETE-запроса, чтобы отправить пользователя на другую страницу или "обновить" текущую.
   
Пример: `return inertia.redirect("ProfilePage");`



