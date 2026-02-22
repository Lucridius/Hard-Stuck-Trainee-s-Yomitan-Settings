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
  - This is mainly for use with [Senren](https://github.com/BrenoAqua/Senren) (but in my setup it doesn't do anything)
  - Just organizes things, gives me extra info if I want it.

## Handle Bar Installation.
Open/download the file ``Modified_JPMNHandles`` and copy the top portion of the file at the top of your handle bars and the bottom portion at the bottom.

<img width="1070" height="351" alt="image" src="https://github.com/user-attachments/assets/d25863e1-121e-437b-a19f-a30ed0c2e173" />


The handle bars I added are at the very end look for ``{{! START OF {conditional-selection-text} HANDLEBAR  }}`` and or ``{{! START OF {conditional-dictionary-name} HANDLEBAR  }}`` and delete them if you want.
## Yomitan Config (anki)
- Have your selection text field or equivalent be ``{conditional-selection-text}``
- Have the main definition be ``{primary-definition}``
- For glossary it's your choice on however you want to set that up
- ([senren](https://github.com/BrenoAqua/Senren)) Have dictionaryPreference be ``{conditional-dictionary-name}``
  - You can add this field to any notetype if you want to for some reason.
**Have all of these set to ``overwrite if available`` (well maybe not glossary actually)

<img width="1236" height="166" alt="image" src="https://github.com/user-attachments/assets/ec67106a-f4e4-423b-b95e-ad8aae1f8fa3" />

## Useage notes.
Assuming you have your selection text field/main definition field set to overwrite if available. <br>
Using a one button setup 
- highlighted text, prints to selection text, main definition will get whatever ``{primary-definition}`` gets.
- You can highlight text, create the card then overwrite the ``{primary-definition}`` result seperately from selection text
  - but not the otherway around, highlighting text will always overwrite ``{primary-definition}``s result

**IF** your yomitan **does not automatically highlight a dictionaries name with a single click/tap** put this CSS at the bottom of your yomitan CSS
```
.tag {
    user-select: all;
}
```

## Quick installation/Useage demonstration
https://github.com/user-attachments/assets/5b444bb0-4a9d-48f2-b13d-00394b7afe10

# CSS
The main bulk of the CSS comes from *again* [AuroraWright](https://gist.github.com/AuroraWright) (see their release of the CSS [here](https://gist.github.com/AuroraWright/563a67c18b8a74ecde3653b7726ff632))
  - *but from them it's just someone else's edited CSS... and that came from someone else yada yada*

## Changes step by step
- Converting it to work with light mode and adding extra compactness (couple other changes)
  - Added a white theme colour at the top of the css, and changed every search result for ``data-theme="dark"`` to ``data-theme="light"``
  - Messed around in ``/* Dual pane layout start */`` to increase compactness to taste.
    - I tried not to change the main CSS with most of my changes but I had to for this.
    - If you want to jump to these changes open 
<img width="1920" height="1080" alt="Untitled(1)" src="https://github.com/user-attachments/assets/b43e15af-437f-4f52-a5d9-bddef118ee89" />

- Adding pitch colouring.
  - Adding CSS to the **TOP** created/edited by [a user from TheMoeWay discord](https://discord.com/channels/617136488840429598/778430038159655012/1365875991741730896).
  - If you want the edited CSS at this point you can open [Base_Edited_CSS.css](https://github.com/Lucridius/Hard-Stuck-Trainee-s-Yomitan-Settings/blob/main/Base_Edited_CSS.css)

<img width="409" height="232" alt="image" src="https://github.com/user-attachments/assets/f83599a3-8cf3-4540-aeb7-291fc041395a" />

### From here it's just additions that go at the **bottom** of the CSS
We'll start with the 2 "feature" CSS additions.

**ウェブ検索 and JMdict Forms [2026-01-14] will always be displayed at the top row (even if only 1 is present)**
  - This is mainly space saving/convience (was more relavent before Searaw from TheMoeWay discord found "masonry"
  - I recommend messing with a custom collapse for JMdict Forms [2026-01-14] until you get a sizing  with it's equal with ウェブ検索
    ```
    .definition-item[data-dictionary='JMdict Forms [2026-01-14]'] {
    --collapsible-definition-line-count: 1.32;
    ```
  - *with this image look aat the top row from the 3 entries*

<img width="1977" height="1540" alt="image" src="https://github.com/user-attachments/assets/de01dd0b-3fd2-4507-a37b-1fce57983451" />

<br>

**デジタル大辞泉 Does not appear in the entry if 大辞泉 第二版 is present**
  - This is just for coverage, they're both like 99% the same except for a few rare cases.
  - Make sure デジタル大辞泉 is higher in your stack then 大辞泉 第二版 for this to work.
    - It's kind of hard to find an example for this, I had when I was testing but I've lost it now

**Jitendex hide example sentences unless you click and hold the entry**

**Remove the link abt the bottom of Jitendex**

**Additional Dictionary/Tag Colouring**

**Expansion arrow changes, moves arrow to the top and removes the blue bar on the right side**
  - This was mainly a change for my old version of the CSS where text could run into the expansion, it no longer does that but it's preference now.
  - **THE RED ARROW IS JUST SEPERATING 2 SEPERATE IMAGES**
  
<img width="244" height="301" alt="image" src="https://github.com/user-attachments/assets/f189e34b-a28d-417e-9c17-f9c1207e6447" />

**TheMoeWay Idle rank colouring CSS**
  - I think it needs a specific version (the latest version)

### **You can find the CSS for all of these changes in BottomOfCSSInserts.css**
