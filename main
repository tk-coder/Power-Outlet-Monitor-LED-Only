/*
  Power Outlet Monitor - LED Only (Nano)
  --------------------------------------
  - Red LED starts fast (~10 Hz) and slows linearly to 1 Hz over 1 hour.
  - Button (D2) confirms alarm.
  - Green LED (D10, PWM) lights constant after confirmation.
*/

#define INTERNAL_LED_PIN 13
#define RED_LED_PIN 11
#define GREEN_LED_PIN 10
#define BUTTON_PIN A2

// --- Red LED blink ---
const unsigned long FAST_BLINK_INTERVAL = 50;   // 10 Hz
const unsigned long SLOW_BLINK_INTERVAL = 500;  // 1 Hz
const unsigned long RAMP_DURATION = 3600000UL;  // 1 hour

// --- Green LED constant brightness ---
const int GREEN_BRIGHTNESS = 80; // adjust 0–255 for desired intensity

// --- State ---
bool alarmActive = true;
bool greenActive = false;
unsigned long blinkStart = 0;
unsigned long lastBlinkTime = 0;
bool redLedState = false;

void setup() {
  pinMode(INTERNAL_LED_PIN, OUTPUT);
  pinMode(RED_LED_PIN, OUTPUT);
  pinMode(GREEN_LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);

  digitalWrite(INTERNAL_LED_PIN, LOW);
  digitalWrite(RED_LED_PIN, LOW);
  analogWrite(GREEN_LED_PIN, 0);

  blinkStart = millis();
  lastBlinkTime = blinkStart;
}

void loop() {
  unsigned long currentMillis = millis();
  unsigned long elapsed = currentMillis - blinkStart;

  // --- Red LED blinking ---
  if (alarmActive) {
    unsigned long blinkInterval;
    if (elapsed >= RAMP_DURATION) {
      blinkInterval = SLOW_BLINK_INTERVAL;
    } else {
      float progress = (float)elapsed / RAMP_DURATION;
      blinkInterval = FAST_BLINK_INTERVAL +
                      (unsigned long)((SLOW_BLINK_INTERVAL - FAST_BLINK_INTERVAL) * progress);
    }

    if (currentMillis - lastBlinkTime >= blinkInterval) {
      redLedState = !redLedState;
      digitalWrite(INTERNAL_LED_PIN, redLedState);
      digitalWrite(RED_LED_PIN, redLedState);
      lastBlinkTime = currentMillis;
    }
  } else {
    digitalWrite(INTERNAL_LED_PIN, LOW);
    digitalWrite(RED_LED_PIN, LOW);
  }

  // --- Button to confirm alarm ---
  if (alarmActive && digitalRead(BUTTON_PIN) == LOW) {
    alarmActive = false;
    greenActive = true;
    analogWrite(GREEN_LED_PIN, GREEN_BRIGHTNESS);
    digitalWrite(INTERNAL_LED_PIN, LOW);
    delay(300); // debounce
  }

  // --- Green LED constant ---
  if (greenActive) {
    // just maintain constant brightness
    analogWrite(GREEN_LED_PIN, GREEN_BRIGHTNESS);
  }
}
