---
layout: post
title: Design Pattern - Singleton
description: >
  A page showing how regular markdown content is styled in Hydejack.
# image: /assets/img/blog/example-content-ii.jpg
sitemap: false
categories: 
    - study
    - spring 
---


# Singleton Pattern

## 1. Singleton Class 란
* 런타임 동안 오직 하나의 인스턴스만 제공하는 클래스 

|Singleton|
|---------|
|- instance: Singleton|
|+ getInstance: Singleton()|


## 2. Singleton 구현 방법 
1. Constructor를 private 하게 선언해서 클래스 밖에서 인스턴스를 만들 수 없도록 한다. 
2. instance가 없으면 생성, 존재하면 기존 instance 반환하는 static method 를 통해서 클래스 밖에서 오직 하나의 인스턴스만 생성, 접근하도록 한다. 

```java:Settings.java 
public class Settings {

    private static Settings instance;

    // 1. private Constructor
    private Settings() {}

    // 2. static method 
    public static Settings getInstance() {
        if (instance == null) {
            instance = new Settings();
        }

        return instance;
    }
}
```

## 3. Thread-Safe 구현 
* 위의 구조가 thread-safe 하지 않은 이유: instnace 생성 전일 때, 두 thread 가 동시에 getInstance() method 내 instance null 체크를 하면 각 thread 입장에서는 조건은 true이다. 따라서 각 thread 는 새로운 instance 를 생성하고, 두 thread 는 서로 다른 instance 를 바라보게 된다. 이는 Singleton pattern 을 만족하지 않는다. 

* 구현 
1. synchronized 키워드 사용
    - 단점: 동기화 메커니즘 처리 과정에서 성능 부하가 생길 수 있다. 
```java
    // 2. static method 
    public static synchronized Settings getInstance() {
        if (instance == null) {
            instance = new Settings();
        }

        return instance;
    }

```

2. eager initialization 
    - 단점: 클래스가 로딩되는 시점에 초기화되며, 사용하지 않는다면 리소스를 낭비하는 일이 될 수 있다. 
```java 
public class Settings {

    private static final Settings INSTANCE = new Settings();

    // 1. private Constructor
    private Settings() {}

    // 2. static method 
    public static Settings getInstance() {
        return INSTANCE; 
    }
}
```

3. double checked locking 
    - 1번 방법보다 효율적, 그 이유: instance 가 이미 있는 경우에는 동기화 메커니즘을 적용하지 않기 때문이다. 
    - 2번 방법보다 효율적, 그 이유: lazy loading; 필요한 시점에 intance를 생성하기 때문에 리소스 절약할 수 있다. 
    - volatile 키워드
```java 
public class Settings {

    private static volatile Settings instance; 

    // 1. private Constructor
    private Settings() {}

    // 2. static method 
    public static Settings getInstance() {
        if (instance == null) {
            synchronized (Settings.class) {
                if (instance == null) {
                    instance = new Settings(); 
                }
            }
        }
    }
}
```


4. (권장하는 방법) static inner 클래스 사용 
```java 
public class Settings {

    // 1. private Constructor
    private Settings() {}

    private static class SettingsHolder {
        private static final Settings INSATNACE = new Setting(); 
    }

    // 2. static method 
    public static Settings getInstance() {
        return SettingsHolder.INSTANCE;
    }
}
```


## 3. Singleton Pattern 을 깨뜨리는 코딩 
1. reflection 
```java:Application.java 
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

public class Application {
    public static void main(String[] args) throws NoSuchMethodException, InvocationTargetException, InstantiationException {
        Settings settings = Settings.getInstance();

        Constructor<Settings> constructor = Settings.class.getDeclaredConstructor();
        constructor.setAccessible(true);
        Settings settings1 = constructor.newInstance();

        // settings != settings1
    }
}
```

2. 직렬화, 역직렬화 사용 

```java:Settings.java 
public class Settings implements Serializable {
...
```

```java:Application.java 
import java.io.*;

public class Application {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        Settings settings = Settings.getInstance();
        Settings settings1 = null;

        try (ObjectOutput out = new ObjectOutputStream(new FileOutputStream("settings.obj"))) {
            // Serialization
            out.writeObject(settings);
        }

        try (ObjectInput in = new ObjectInputStream(new FileInputStream("settings.obj"))) {
            // Deserialization
            settings1 = (Settings) in.readObject();
        }

        // settings != settings1 
    }
}
```



<!-- ## Note 

1. enum 을 사용하지 않고 싱글톤 패턴을 구현하는 방법은?
2. private 생성자와 static 메서드를 사용하는 방법의 단점은? 
3. enum을 사용해 싱글톤 패턴을 구현하는 방법의 장단점? 
4. static inner 클래스를 사용해 싱글톤 패턴 구현

-->


## 4. Spring 에서 design pattern 
