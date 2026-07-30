# Third Eye for The Blind
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Eddie K. | Cupertino High School | Bio-Engineering | Incoming Sophomore

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone
Assembling hardware and adding straps 
Sensors such as vibration and beeps
Walking / practical experiment
Develop hand straps and hardware


**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

First Milestone Highlights:

Project: Third Eye for The Blind

Progress:
- Implemented three different components in correspondence with the ultrasonic sensors (LED, Buzzer, Vibration motor)
- Soldered all wiring onto the official pref board 
- Planned schematics for design
- Developed coding on breadboard and tested for functiosn
  
Challenges:
- Multimeter testing and real function testing on the pref board
- Permanent project building with wearable design
- Building multiple projects for both hands (maybe all limbs)

Plans:
- Record code process and design measurements on notebook
- Search online for reference schematics
- Ask help and double-confirm with instructors before making permanent decisions

# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/Va0Sycy-55k?si=388BVatnQnXsj7uk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Starter Project Highlights:

Progress:
- Soldered RBG lights and sliders onto the board
- Functions work as sliders combine


# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

<img width="1762" height="1202" alt="Screenshot 2026-07-09 153159" src="https://github.com/user-attachments/assets/9e8f3aa0-4e09-46b3-9fec-938d7251222e" />


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
// Pin Definitions
const int trigPin = 9;
const int echoPin = 10;
const int buzzer = 4;      
const int ledPin = 11;     
const int vibPin = 5;      // Added Vibration Motor Pin
const int btnLed = 2;
const int btnBuzz = 3;
const int btnVib = 6;      // Added Pin for Vibration Button

// Modes
bool ledMode = false;
bool buzzMode = false;
bool vibMode = false;      // Added Vibration Mode

// State Tracking
bool lastBtnLed = HIGH;
bool lastBtnBuzz = HIGH;
bool lastBtnVib = HIGH;    // Added State tracking for Vib Button
unsigned long lastBeepTime = 0;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(vibPin, OUTPUT); // Set Vib Pin as Output
  pinMode(btnLed, INPUT_PULLUP);
  pinMode(btnBuzz, INPUT_PULLUP);
  pinMode(btnVib, INPUT_PULLUP); // Set Vib Button
}

void loop() {
  // --- BUTTON TOGGLE LOGIC ---
  if (digitalRead(btnLed) == LOW && lastBtnLed == HIGH) { ledMode = !ledMode; delay(50); }
  lastBtnLed = digitalRead(btnLed);

  if (digitalRead(btnBuzz) == LOW && lastBtnBuzz == HIGH) { buzzMode = !buzzMode; delay(50); }
  lastBtnBuzz = digitalRead(btnBuzz);

  if (digitalRead(btnVib) == LOW && lastBtnVib == HIGH) { vibMode = !vibMode; delay(50); }
  lastBtnVib = digitalRead(btnVib);

  // --- SENSING LOGIC ---
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  long duration = pulseIn(echoPin, HIGH, 30000); 
  int distance = (duration == 0) ? 999 : (duration / 2) / 29.1;

  // --- OUTPUT LOGIC ---
  if (distance > 0 && distance < 20) {
    // LED
    analogWrite(ledPin, ledMode ? map(constrain(distance, 1, 20), 1, 20, 255, 50) : 0);
    
    // Vibration Motor: Proportional strength (analog)
    // Note: If your motor isn't strong enough at low values, increase the minimum '50'
    analogWrite(vibPin, vibMode ? map(constrain(distance, 1, 20), 1, 20, 255, 100) : 0);
    
    // Buzzer
    if (buzzMode) {
      int targetFreq = map(constrain(distance, 1, 20), 1, 20, 3000, 100);
      int interval = map(constrain(distance, 1, 20), 1, 20, 50, 500);
      if (millis() - lastBeepTime >= interval) {
        tone(buzzer, targetFreq, 50); // Simplified tone
        lastBeepTime = millis();
      }
    } else {
      noTone(buzzer);
    }
  } else {
    analogWrite(ledPin, 0);
    analogWrite(vibPin, 0);
    noTone(buzzer);
  }
}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| 4mm LED | Visual indicator | $7.99 | <a href="https://www.amazon.com/300-Pcs-LED-Diode-Assortment/dp/B0F38LJDJB/ref=sr_1_3?crid=3FW43FZ2KRTXG&dib=eyJ2IjoiMSJ9.JsY0cBJjZq_qIrS5ffXS7GQ6AH0f45-KVj00jWpQ2EUO-zDxUILBC9SNxQq4rtxWPCZzv_j0ITFM_U3ZV-kVMnfROAZs5BgyGXWqLbtXCU3wcuHE7Mirm4ih8jT0q6tl_7VJOVXYkEKrTVrfakbZfKmMWwFh45noFSQgbdhOPHkwBf0NU55uYbRd4dIb6wpgnRzXamVwMvW7H3eFJlTGA8OO-Civ8lZz-LjZOjuUdHk.i3tE-taNCqSiBkmGzuqDnQfer73whfqv_i9YCznrkf8&dib_tag=se&keywords=4mm+led&qid=1785433989&sprefix=4mm+l%2Caps%2C163&sr=8-3"> Link </a> |
| HC-SR04 Ultrasonic Sensor | Distance Detection | $6.99 | <a href="https://www.amazon.com/WWZMDiB-HC-SR04-Ultrasonic-Distance-Measuring/dp/B0B1MJJLJP/ref=sr_1_3?crid=5T7AAISB3ULS&dib=eyJ2IjoiMSJ9.w-v74CMMP9eRh1BFF5BJ6xZlNH9LlX5HLX1Axp43FWbulHD6ja5itA3w3JVxWr5oewZ6088SCihxTf3Bbk4-DKK01cDJftQ06K9TurFcR2OJDgJaFPI4_ZymNnIfU7qtgkvE42oAEC4Duu5Vfcgi5xz1GnWkmA63eQJeLQdaNdKtYcG1TEavzYBdIPKzHsj2EFaO2b7aLoP7Dg9eg06Ch2Q2MONSHUxdtAtrvua_bDI.IM1wVC_DKrjok0s83nu3w2sbpeZds_HnfX7FQK1HURY&dib_tag=se&keywords=ultrasonic%2Bsensor&qid=1785434052&sprefix=ultrasonic%2Bsen%2Caps%2C182&sr=8-3&th=1"> Link </a> |
| Jumper Wires Generic | General wiring connection | $3.99 | <a href="https://www.amazon.com/California-JOS-Breadboard-Optional-Multicolored/dp/B0BRTHR2RL/ref=sr_1_4?crid=VSUTI3XYIF2W&dib=eyJ2IjoiMSJ9.QGbaFF62mgZ1Tf0J7CajkBnivKMOTOpZJUS1O07RvMRm699JAAkLHqyXCFYTEhIDsEnwupE57VpPhtqDGpYHYC6SUhEV6n9ZEq7wHYceNxnonz0QCV0YAQ9jsgH3J_rIy8ICuGCiobaArsuMDZLKWQHSk17dxpj-DmzKu1vjaObLp82s2ZlGN2oXyEWB13hqj93vlNguZ4CuEFNhT_-TV0pI-pjlEU24m9lxJRPpg_s.33jLmrbTm68ihWCBTaM9sr8lj0_5Il1cabJaPv-YTCM&dib_tag=se&keywords=jumper%2Bwires%2Bgeneric&qid=1785434098&sprefix=jumperwires%2Bgeneri%2Caps%2C168&sr=8-4&th=1"> Link </a> |
| Arduino NaNO - 5V/16MHz | Microcontroller | $19.30 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/Arduino-ABX00083-Bluetooth-MicroPython-Compatible/dp/B0C947BHK5/ref=sr_1_1?crid=1WM6BIWEBWM1S&dib=eyJ2IjoiMSJ9.QmNYvO8VeEYJRoPLV8e0zctqT2oRtwroDCO2-jHie3NoEcQNo9t2nd1SBRx-w6U12VN39UNF1dzmbioDFPjFRk7LVO3tPVOn_RiZJDgPJQAfF1goW6h4qwC3qV2zHMyl36JTXJWk0HYBZCZ2dA7ZeC-DcrIiSD-sVaVhtQiW23_vy9j-UnmJrjXlqns1JM3GXVQede4ktiFrfnJCjV-Zr7s2HQkSs0YOqcCk5HIKRyw.A5tgdmvESqimesrp6hMD0yfWSVS_Co0AEcOTXaQql_s&dib_tag=se&keywords=arduino%2Bnano&qid=1785434268&sprefix=arduino%2Bnan%2Caps%2C179&sr=8-1&th=1)"> Link </a> |
| Wrist Strap | Device anchor-part | $5.89 | <a href="https://www.amazon.com/Adjustable-Weightlifting-Tendonitis-Relief-Wear-Anywhere-Unisex/dp/B08LCJT6DK/ref=sr_1_13?crid=19NREG6WG80SU&dib=eyJ2IjoiMSJ9.8r8AcuJ1CRP7lCcc7bT0UsVdGbozW5dpxlnz04QL47z46cAmrbwYDvM1lWoNWc6CPh0F7uWwqmPSLDsEZQyWzknlVW1eVAm5n3NOfMDR8O0xf27QFUIK1FUaDKM2Bhg3jwxaMVUV4cR-iT-GjBVCHqElfqURjYtKKzzWJWX3n8eWu0IVCwSb2FUuqFmGxM41wEKmael4QdbOKp1iUE9sfT895nH3RjvQd1_-OkfEdfckntGMtsS0YVlL9oTiEitWsl0AYICO7S1lutPFTfttBT70gh45P0XBownnzawCOz8.oK7KKXd6r8Bfmb2f2GojjhrsEuRBnJa1pc8v0LBimAk&dib_tag=se&keywords=wrist+strap&qid=1785434311&sprefix=wrist+strap%2Caps%2C188&sr=8-13"> Link </a> |
| Piezo Buzzer | Sound indicator | $6.99 | <a href="https://www.amazon.com/mxuteuk-Electronic-Computers-Printers-Components/dp/B07VK1GJ9X/ref=sr_1_6?crid=UUOHYDK2IF21&dib=eyJ2IjoiMSJ9.Kc1lRhz-FXgslMSBkHup9x5It0lsf8CxJn4BUQ5uZ9kUnt23DKdB3bYOhwZTmRyvpFn-DKD6m99pFbj7aJqN8KjZ4jxRbUzwZlBP6UCVLqgNHcO-9rFfTpbabEGbm4OPT1hBazXvTNjgCqFmAVYl5tEUJxbT3LR8jhwglOa3xAB3wsyfDdM_n2ViTgBdTq8T-M_V4335r62gCJYFABvfkkEEZUJx7BxF-gF4RLK5Xyo.8qvmTHCXpQWBfmUF4MhXyMyfgyHSEoh8NLrkR6u4i-U&dib_tag=se&keywords=piezo+buzzer&qid=1785434373&sprefix=piezobuzzer%2Caps%2C173&sr=8-6"> Link </a> |
| Perf Board | Device wiring board | $8.79 | <a href="https://www.amazon.com/ElectroCookie-Solderable-Breadboard-Electronics-Gold-Plated/dp/B07ZV8FWM4/ref=sr_1_3?crid=2KY6VCIFC5GX8&dib=eyJ2IjoiMSJ9.ChrcuHWMpTILCAyeKEYGp-h0Zwt0JMEaKZMlTlpjcTefqHkcEXl2ICWLP_6aBIu7bHJ4NDOM_2FrfN4WkyCIjKFDmhATr_RZkBK6BbMPSGu_WxfznxPi96P2OxP39Apsgal4ins6yjBFCD71KhY9b_W9kjSAijaYkVdfPRk38gpzkvxLiZESxKoG6lFE6UPybB6wx5_ycFa2qMRZ1iNaWEM9JuFsrYBpaEbuWlmE92Y.RJZ51I5pZQtoyFOx65kITesLcXVq9IOVEnH9eyNNCuY&dib_tag=se&keywords=solderable%2Bbreadboard&qid=1785434406&sprefix=solderable%2Bbreadboar%2Caps%2C185&sr=8-3&th=1"> Link </a> |
| Push Buttons | Detection mode trigger | $4.99 | <a href="https://www.amazon.com/DAOKI-Miniature-Momentary-Tactile-Quality/dp/B01CGMP9GY/ref=sr_1_9?crid=3GJYX0XNXY7VG&dib=eyJ2IjoiMSJ9.qy3w6AeDbDUo58qX8hVJKZH1S5oEc59cOHIdoe7gTMy7EZzZdfiv3uvn9NB9JKB7AIsxZMMY3CHWGk8Fh8M6m3TZeXiXJWU6Kg1IIe_GlTBSDPWiW0ip-Z99543zA7fUwBzzgDTysX_cowYPbuqQ8gFiSb7E0VPEZ2StjCfLvXxKU2sTDOwg1YonUDdKV1LnW7otQjRNuDzHSUW1qqWCpbcqyixAGAWJASjKhbuVeOQ.sJTtv_IDfUn_zs8TWt7OXacbvFPoIPfGin7AR4_H5nY&dib_tag=se&keywords=push%2Bbuttons&qid=1785434437&sprefix=push%2Bbuttons%2Caps%2C188&sr=8-9&th=1"> Link </a> |
| Power Bank | Power supply | $21.99 | <a href="https://www.amazon.com/INIU-Portable-High-Speed-Flashlight-Compatible/dp/B0CB1FW5FC/ref=sr_1_3?crid=2I0AUZM49T16&dib=eyJ2IjoiMSJ9.sldn4xwEUzUGT4FndQzSHhB2nMYEMmo_azVOknkb8h9VTFfCxhXbZgMa3hSm0TtiMooTB3G5EeNAlE6U0pcnKJqJNWfT4QlMzO0tF_2WVwCXBUSo1usIVuHY088qAFkUUj4GTsmI7dgQ7xj750nA6IIaV_41BTJf2dZ3DT6unxC8KVL4FTWldMK3np_AVa0m_j3hAa5EfzWFUwBTVHGVp-RVDPvx6AuiBkZySc8QtB8.zYEf0ZnTE-U6mohK6vxqYQ9JxOPcp5b_7cgQJQ-w-E8&dib_tag=se&keywords=power%2Bbank&qid=1785434468&sprefix=power%2Bban%2Caps%2C209&sr=8-3&th=1"> Link </a> |
| Coin Vibration Motor | Physical indicator | $5.99 | <a href="https://www.amazon.com/DIANN-Vibration-Button-Type-Vibrating-Appliances/dp/B0B4SMZCPW/ref=sr_1_9?crid=2MCVOK5J26ALV&dib=eyJ2IjoiMSJ9.FV7YrAS3AQCVlisBCD0PfLbuahj4o_3IC0z0KrbsGBfXtpoZ30oz0Sjxrwitt7omQuu56q6g_D190QJO6RrBLJTy-3sGYyAa56JOhMLfypRS7O9S2IlvwADR7Wb_17bj95v02lSN0MSWFasWAs2miDCnwWXYya0sD2FzYgxAodddUqhd6Whffh9gvwE7VOqq0LyGuL_keoc7UIdoGpjutScwRj9mqPqBSpfQEC9U34YE6BJ2jUMitwoqkf7s5ljuXx0IxvNSin0CEgvf29LLnQ_nGJHPGp0kGNdPE8Shlgk.nx1NxZlOfSDk1-QJJuZw1rGtQMDdqe2oF8m2HpeceWA&dib_tag=se&keywords=vibration%2Bmotor&qid=1785434498&sprefix=vibration%2Bmoto%2Caps%2C180&sr=8-9&th=1"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
