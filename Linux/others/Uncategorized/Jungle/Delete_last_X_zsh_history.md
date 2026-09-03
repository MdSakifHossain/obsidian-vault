# How to Delete last X zsh history

## **Mental Model**

**Two Things to Remember:**

- Hard Copy (The History File)
- Soft Copy (Termianls Memory)

| Action                      | What happens                 |
| --------------------------- | ---------------------------- |
| **Open new terminal**       | File → Memory (read)         |
| **Type commands**           | Memory only (file unchanged) |
| **Close terminal normally** | Memory → File (append)       |
| **Manual sync**             | Memory → File (write full)   |
| **Manual reload**           | File → Memory (re-read)      |

shell memory has the latest stuff, i have to tell the memory to write it down. now they are in sync. then i have to clean the history file and then i tell the memory to forget what you know and this is the new list. and memory gets a new memory. And thats all it is...

