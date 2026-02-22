# Hard-Stuck-Trainee's-Yomitan-Configuration
This page is broken up into 2 main sections
- Handle bars
- Yomitan CSS
<img width="834" height="736" alt="image" src="https://github.com/user-attachments/assets/a4e3a598-1395-47d7-b00b-6f06099a4330" />

# Handle Bars
The main portion of the handle bars was done by [AuroraWright](https://gist.github.com/AuroraWright) and you can view those original handle bars [here](https://gist.github.com/AuroraWright/8f529e7ec5a47bfa5d979821541562a5). From here I'll just call them JPMNHandles
(I'm assuming you're already familiar with how yomitan works)
The main advantage of these handlebars comes from the addition of ``{primary-definition}`` and ``{secondary-definition}``

``{primary-definition}`` Has a variety of features baked into it.
- If highlighted text matches a dictionary name it will output that dictionary **(configurable setting)** 
  - (I think this is how yomitan should work personally)
- Sends the highlighted text to the anki field **(configurable setting)** *(if it's not a dictionary name)* 
  - effectivly the same as ``{popup-selection-text}`` except you can't really use it in that field (if ur note type supports it)
- If the highlighted text is matched to a dictionary result, will output that dictionary and bold the highlighted text **(configurable setting)**
  - This I think is the best way to use selected text from the JPMNHandles **HOWEVER** it's prone to failing to match *(due to CSS ect)* and will then result in just printing the default dictionary.
- ``{primary-definition}``/``{secondary-definition}`` Can output the TOP dictionary from your results either bio or mono (they each do the other) **(configurable setting)**
  - You can set ignore'd dictionaries ect, pretty good fallback.
<img width="1394" height="714" alt="image" src="https://github.com/user-attachments/assets/ae71e5e3-94d7-42c8-a474-4c2ca26ad0da" />

## The problem(s)
As I mentioned,
- with these handlebars alone you can't send Selected Text to the selected text anki field.
- if you're using the bolding feature and it fails you just get a defaulted dictionary, and no selected text **at all**
## My addition(s)
I've added 2 handle bars (chatgpt) 
### ``{conditional-selection-text}``
Being seperated from ``{primary-definition}`` gives us back the freedom to use a ``{popup-selection-text}`` style handlebar.
- If matched text matches a dictionary name **Nothing** will happen.
- If highlighted text is anything else, will output it to the field.
  - The main advantage here for me is you can continue to use the bolding defintion match feature, but you also will always get selection text even if the bolding match fails.
  - I'm just OCD braind and want to use the selection text field.
###``conditional-dictionary-name}``###
This is really just an OCD feature you can feel free to delete (I imagine pretty much noone will use it)
- If matched text is a dictionary name, will output it.
- If ``{primary-definition}`` correctly matches bolding text highlight, will output that dictionaries name.
- If no dictionaries are matched outputs in plain text "Defaulted"
  - This is mainly for use with Senren (but in my setup it doesn't do anything)
  - Just organizes things, gives me extra info if I want it.

## Handle Bar Installation.
Open/download the file ``Modified_JPMNHandles`` and copy the top portion of the file at the top of your handle bars and the bottom portion at the bottom.
The handle bars I added are at the very end look for ``{{! START OF {conditional-selection-text} HANDLEBAR  }}`` and or ``{{! START OF {conditional-dictionary-name} HANDLEBAR  }}`` and delete them if you want :shrug:
## Yomitan Config (anki)
- Have your selection text field or equivalent be {conditional-selection-text}
- Have the main definition be ``{primary-definition}``
- For glossary it's your choice on however you want to set that up
- (senren) Have dictionaryPreference be ``{conditional-dictionary-name}``
  - You can add this field to any notetype if you want to for some reason.
**Have all of these set to ``overwrite if available``
## Quick installation/Useage demonstration
https://github.com/user-attachments/assets/5b444bb0-4a9d-48f2-b13d-00394b7afe10

# CSS

