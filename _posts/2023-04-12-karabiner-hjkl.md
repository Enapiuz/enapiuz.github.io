---
layout: post
title: Second layer of keys for macOS
published: true
---

I've always wanted to buy 40% ortholinear keyboard.
But due to the fact that I move from one
location to another quite often I can't have that luxury. So I just use my MacBook.

But there is still a way to, let's say, emulate it.

40% keyboards have really few keys and due to that fact you need a workaround
to get access to absent keys.  
It's called layers.  
But there might be another reason you want to use layers even on fully-sized keyboards.

I quite often use arrow keys. And I have to move my right hand down in not
the most natural way. At the same time I like H/J/K/L navigation.  
So I just made CapsLock to be my sort of "second layer switcher".

## What to do

First of all you need [Karabiner Elements](https://karabiner-elements.pqrs.org)

Then you need to disable CapsLock in macOS settings.  
It's not mandatory but otherwise will cause a lot of pain.

![macos-settings.png]({{ site.baseurl }}/images/macos-settings.png)

And in the end drop this json into complex_modifications of your karabiner.json

karabiner.json:
```json
{
  "global": {
    // ...
  },
  "profiles": {
    "complex_modifications": {
      "parameters": {
        // ...
      },
      "rules": [
        // Drop it here
      ]
    }
  }
}
```

HJKL config:
```json
{
  "description": "Change Caps Lock + H/J/K/L to Arrow Keys",
  "manipulators": [
    {
      "from": {
        "key_code": "caps_lock",
        "modifiers": {
          "optional": [
            "any"
          ]
        }
      },
      "to": [
        {
          "set_variable": {
            "name": "caps_arrows_mode",
            "value": 1
          }
        }
      ],
      "to_after_key_up": [
        {
          "set_variable": {
            "name": "caps_arrows_mode",
            "value": 0
          }
        }
      ],
      "to_if_alone": [
        {
          "key_code": "caps_lock"
        }
      ],
      "type": "basic"
    },
    {
      "conditions": [
        {
          "name": "caps_arrows_mode",
          "type": "variable_if",
          "value": 1
        }
      ],
      "from": {
        "key_code": "j",
        "modifiers": {
          "optional": [
            "any"
          ]
        }
      },
      "to": [
        {
          "key_code": "down_arrow"
        }
      ],
      "type": "basic"
    },
    {
      "conditions": [
        {
          "name": "caps_arrows_mode",
          "type": "variable_if",
          "value": 1
        }
      ],
      "from": {
        "key_code": "k",
        "modifiers": {
          "optional": [
            "any"
          ]
        }
      },
      "to": [
        {
          "key_code": "up_arrow"
        }
      ],
      "type": "basic"
    },
    {
      "conditions": [
        {
          "name": "caps_arrows_mode",
          "type": "variable_if",
          "value": 1
        }
      ],
      "from": {
        "key_code": "h",
        "modifiers": {
          "optional": [
            "any"
          ]
        }
      },
      "to": [
        {
          "key_code": "left_arrow"
        }
      ],
      "type": "basic"
    },
    {
      "conditions": [
        {
          "name": "caps_arrows_mode",
          "type": "variable_if",
          "value": 1
        }
      ],
      "from": {
        "key_code": "l",
        "modifiers": {
          "optional": [
            "any"
          ]
        }
      },
      "to": [
        {
          "key_code": "right_arrow"
        }
      ],
      "type": "basic"
    }
  ]
}
```

And that's it!
