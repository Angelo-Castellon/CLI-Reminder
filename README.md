# CLI Reminder

A simple command-line reminder tool built with Go that schedules desktop notifications for future times using natural language parsing.

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white) ![CLI](https://img.shields.io/badge/CLI-Tool-blue?style=for-the-badge)

## 🎯 Overview

CLI Reminder is a lightweight command-line application that allows you to set reminders using natural language time descriptions. The tool runs in the background and displays a desktop notification when the specified time arrives.

**Key Features:**
- 📅 Natural language time parsing ("in 5 minutes", "at 3:30pm", "tomorrow at 9am")
- 🔔 Desktop notifications with custom messages
- ⚡ Runs as background process
- 🕐 Automatic time validation (prevents past times)

## 🚀 Tech Stack

- **Language**: Go (Golang)
- **Time Parsing**: olebedev/when (natural language date/time parser)
- **Notifications**: gen2brain/beeep (cross-platform desktop notifications)

## 📦 Installation

### Prerequisites

- Go 1.16 or higher installed
- macOS, Linux, or Windows with notification support

### Install Dependencies
```bash
# Clone the repository
git clone https://github.com/Angelo-Castellon/CLI-Reminder.git
cd CLI-Reminder

# Initialize Go module and install dependencies
go mod init CLI-Reminder
go get github.com/gen2brain/beeep
go get github.com/olebedev/when
```

### Build the Application
```bash
# Build executable
go build -o reminder main.go

# Optional: Install globally (Linux/macOS)
sudo mv reminder /usr/local/bin/
```

## 💻 Usage

### Basic Syntax
```bash
./reminder <time> <message>
```

### Examples

**Set reminder in relative time:**
```bash
./reminder "in 5 minutes" "Take a break"
./reminder "in 2 hours" "Meeting with team"
./reminder "in 30 seconds" "Test notification"
```

**Set reminder at specific time:**
```bash
./reminder "at 3:30pm" "Doctor appointment"
./reminder "at 14:00" "Lunch time"
./reminder "tomorrow at 9am" "Morning standup"
```

**Natural language expressions:**
```bash
./reminder "next monday at 10am" "Weekly review"
./reminder "tonight at 8pm" "Call mom"
./reminder "in half an hour" "Check oven"
```

### How It Works

1. **Parse Command**: The tool parses the time argument using natural language processing
2. **Validate Time**: Ensures the specified time is in the future
3. **Background Process**: Spawns a background process that sleeps until the reminder time
4. **Display Notification**: Shows a desktop notification with your custom message

### Output Example
```bash
$ ./reminder "in 5 minutes" "Drink water"
Reminder will be displayed after 5m0s
```

After 5 minutes, a desktop notification appears with the message "Drink water".

## 🛠️ Technical Details

### Time Parsing

The application uses the `olebedev/when` library with English and common language rules to parse various time formats:

- **Relative times**: "in X minutes/hours/days"
- **Absolute times**: "at HH:MM", "at 3pm"
- **Natural language**: "tomorrow", "next week", "tonight"

### Background Execution

The tool uses a clever self-spawning technique:
1. First execution validates and spawns a background process
2. Background process inherits the command with a special environment variable
3. Background process sleeps until reminder time
4. Displays notification and exits

### Environment Marker

Uses `GOLANG_CLI_REMINDER=1` environment variable to distinguish between parent and background processes.

## 📂 Project Structure
```
CLI-Reminder/
├── main.go              # Main application logic
├── go.mod               # Go module dependencies
├── assets/
│   └── information.png  # Optional notification icon
└── README.md            # Project documentation
```

## 🔧 Configuration

### Custom Notification Icon

Place your custom icon in `assets/information.png` or modify the path in the code:
```go
err = beeep.Alert("Reminder", message, "assets/your-icon.png")
```

### Change Notification Title

Edit the alert title in `main.go`:
```go
err = beeep.Alert("Your Custom Title", message, "assets/information.png")
```

## 🎓 What I Learned

- **Natural Language Processing**: Using NLP libraries to parse human-readable time formats
- **Process Management**: Spawning and managing background processes in Go
- **Cross-Platform Desktop Notifications**: Implementing system notifications on multiple OS platforms
- **Time Manipulation**: Working with Go's `time` package for duration calculations and comparisons
- **Environment Variables**: Using environment markers to control program flow
- **Error Handling**: Implementing proper error handling with informative exit codes
- **Command-Line Arguments**: Parsing and validating CLI input in Go

## ⚙️ Error Codes

| Exit Code | Description |
|-----------|-------------|
| `0` | Success - reminder scheduled |
| `1` | Invalid arguments (missing time or message) |
| `2` | Time parsing error or unable to parse time |
| `3` | Specified time is in the past |
| `4` | Notification display error |
| `5` | Background process spawn error |

## 🐛 Troubleshooting

**Notification not appearing?**
- Ensure notification permissions are enabled for terminal/command prompt
- Check if `beeep` library supports your OS notification system

**"Unable to parse time" error?**
- Try different time formats: "in 10 minutes" instead of "10 minutes"
- Use absolute times: "at 3:30pm" instead of "3:30"

**"Set a future time!" error?**
- The specified time is in the past
- For times like "3pm", if it's already past 3pm, try "tomorrow at 3pm"

## 📚 Dependencies
```go
github.com/gen2brain/beeep    // Desktop notifications
github.com/olebedev/when      // Natural language date/time parser
```

## 🔮 Future Enhancements

Potential improvements for learning purposes:

- [ ] Add recurring reminders (daily, weekly)
- [ ] Store reminders in a database for persistence
- [ ] List all active reminders
- [ ] Cancel/delete scheduled reminders
- [ ] Add sound notifications
- [ ] Create configuration file for default settings
- [ ] Add timezone support
- [ ] Implement snooze functionality
- [ ] Create web UI for managing reminders
- [ ] Add calendar integration (Google Calendar, Outlook)

## 🌐 Platform Support

| Platform | Notification Support |
|----------|---------------------|
| macOS | ✅ Native notifications |
| Linux | ✅ libnotify/notify-send |
| Windows | ✅ Windows toast notifications |

## 🤝 Contributing

This is a learning project, but suggestions and improvements are welcome! Feel free to fork and experiment.

## 📄 License

This project is open source and available for educational purposes.

---

**Built with** ⏰ **while learning Go system programming and CLI tools**
