# Designing a Browser History Feature

The tutorial addresses the task of designing a browser history management system, focusing on the implementation of functionalities like visiting a new webpage, navigating backward, and moving forward through the history.

## Objective

The goal is to create a class capable of handling browser history operations, including initializing the browser with a homepage, visiting new URLs, and enabling backward and forward navigation.

## Key Components

- **Constructor**: Initializes the browser with a specified homepage.
- **Visit(URL)**: Navigates to a new URL, updating the browser's current position in history.
- **Back(steps)**: Moves backward a specified number of steps in history and returns the current URL.
- **Forward(steps)**: Moves forward a specified number of steps in history and returns the current URL.

## Implementation

The implementation utilizes a doubly linked list to store visited URLs, facilitating efficient backward and forward navigation.

```java
class BrowserHistory {
    class Node {
        String url;
        Node prev, next;

        public Node(String url) {
            this.url = url;
        }
    }

    private Node current;

    public BrowserHistory(String homepage) {
        current = new Node(homepage);
    }

    public void visit(String url) {
        Node newNode = new Node(url);
        current.next = newNode;
        newNode.prev = current;
        current = newNode; // Move forward to the new page
    }

    public String back(int steps) {
        while (current.prev != null && steps-- > 0) {
            current = current.prev;
        }
        return current.url;
    }

    public String forward(int steps) {
        while (current.next != null && steps-- > 0) {
            current = current.next;
        }
        return current.url;
    }
}
```
## Example Usage

```java
BrowserHistory browserHistory = new BrowserHistory("takeuforward.org");
browserHistory.visit("google.com"); // User visits 'google.com'.
browserHistory.visit("instagram.com"); // User then visits 'instagram.com'.
browserHistory.back(1); // User goes back one step to 'google.com'.
browserHistory.back(1); // User goes back another step to 'takeuforward.org'.
browserHistory.forward(1); // User moves forward to 'google.com' again.
browserHistory.visit("takeuforward.org"); // User visits 'takeuforward.org', overwriting forward history.
browserHistory.forward(2); // No forward history, remains on 'takeuforward.org'.
browserHistory.back(2); // User goes back to 'google.com'.
browserHistory.back(7); // Attempts to go back 7 steps but only goes back to the homepage.
```

## Complexity Analysis

Constructor: O(1), as it only involves initializing a single node.
Visit(URL): O(1), since adding a new node to a doubly linked list is a constant time operation.
Back(steps) and Forward(steps): O(steps), proportional to the number of steps taken, due to traversal through the linked list.
This design effectively mirrors how real web browsers manage history, offering an intuitive navigation experience while ensuring efficient operations.
