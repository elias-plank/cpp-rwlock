# ReadWriteLock - A C++20 Read-Write Lock Utility

`ReadWriteLock` is a header-only C++20 utility that provides a lightweight, RAII-based mechanism for managing access to
shared data using a `std::shared_mutex`. It offers both **exclusive (write)** and **shared (read)** access using a
type-safe and simple interface.

## Key Features:

- **RAII-based locking**: The lock is automatically released when it goes out of scope.
- **Read-Write Locking**: Supports both exclusive locks for writing and shared locks for reading.
- **Concepts-based type safety**: Leverages C++20 concepts to ensure that locks are used in a type-safe manner.
- **Header-only**: No compilation or linking required; just include the header file.

---

## Example Usage

```cpp
#include "rwlock.hpp"

struct Person {
    std::string name;
    std::int32_t age;
};

void run() {
    ReadWriteLock<Person> person{
        "Elias", 20
    };
    
    std::jthread writer([&person]() {
        // Exclusively lock the shared resource 
        auto lock = person.lock();
        lock->name = "Elias Engelbert";
        lock->age++;
        std::printf("Writer updated the person.\n");
    });
    
    std::jthread reader([&person]() {
        // Shared lock for read access
        auto lock = person.shared_lock();
        std::printf("Reader sees: %s, %d\n", lock->name.c_str(), lock->age);
    }); 
}
```