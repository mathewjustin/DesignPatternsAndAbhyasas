# What are design patterns

Design patterns are general reusable solutions to common problems that occur in software design. They are not code, but rather guidelines on how to solve a particular problem in a particular context. They are not a finished design that can be transformed directly into code. They are a description or template for how to solve a problem that can be used in many different situations.


# Types of design patterns in Java

There are three types of design patterns in Java:
* Creational
* Structural
* Behavioral

# Creational design patterns

Creational design patterns are concerne# What are design patterns

Design patterns are general reusable solutions to common problems that occur in software design. They are not code, but rather guidelines on how to solve a particular problem in a particular context. They are not a finished design that can be transformed directly into code. They are a description or template for how to solve a problem that can be used in many different situations.


# Types of design patterns in Java

There are three types of design patterns in Java:
* Creational
* Structural
* Behavioral

# Creational design patterns

Creational design patterns are related to the way of creating objects. These patterns provide various object creation mechanisms, 
which increase flexibility and reuse of existing code. 
These patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code.

There are five types of creational design patterns:

* Singleton Method
* Factory Method
* Abstract Factory Method
* Builder Method
* Prototype Method

## Singleton Method
 
Consider a scenario where you need to manage
a configuration file. You need to read the configuration file only once and then keep it in memory.
For this, you need to create a class that will read the configuration file and keep it in memory.

![](/Users/justin/Documents/dating-app/DsAndAlgo-2024/DSAndAlgo/DesignPatternsAndAbhyasas/JDP-Java_Design_Patterns/singletom-puml.png)

Example: Java Runtime, Logger, Spring Beans, and many more.

Different flavours from JDK.

Runtime.getRuntime();
Desktop.getDesktop();

```java
import java.util.HashMap;
import java.util.Map;

public class ConfigurationManager {
    // The static variable that stores the singleton instance
    private static ConfigurationManager instance = null;
    
    // A map to store the key-value pairs from the configuration file
    private Map<String, String> configData;
    
    // Private constructor to prevent instantiation from outside the class
    private ConfigurationManager() {
        configData = new HashMap<>();
        readConfigurationFile();
    }
    
    // Public method to return the singleton instance
    public static synchronized ConfigurationManager getInstance() {
        if (instance == null) {
            instance = new ConfigurationManager();
        }
        return instance;
    }
    
    // Simulates reading the configuration file and storing its contents
    private void readConfigurationFile() {
        // Simulated configuration data
        configData.put("key", "value");
        // Add actual file reading logic here
    }
    
    // Public method to get a configuration value by key
    public String getConfigValue(String key) {
        return configData.getOrDefault(key, "Key not found");
    }
    
    // Example usage
    public static void main(String[] args) {
        ConfigurationManager configManager = ConfigurationManager.getInstance();
        String value = configManager.getConfigValue("key");
        System.out.println("The value for 'key' is: " + value);
    }
}
```

