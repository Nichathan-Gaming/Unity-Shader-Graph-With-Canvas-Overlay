# Unity-Shader-Graph-With-Canvas-Overlay
This repository will give detailed instructions on how to apply a *Shader* created with the *Shader Graph* window to an element on a *Canvas* with the *render mode* set to *screen space : overlay*. This repository will also be used as a supplement for the [YouTube video](https://youtu.be/n77mW90Dr8g).

## Table Of Contents
1. **[Initial Setup and Details](#Initial-Setup-and-Details)**
   1. **[Disclaimer](#Disclaimer)**
   2. **[Details](#Details)**
   3. **[Before continuing you should have](#Before-continuing-you-should-have)**
2. **[Instructions](#Instructions)**


## 1 Initial Setup and Details
### 1.1 Disclaimer
To the best of my knowledge, this walkthrough and all content inside of it has been typed with no errors or misinformation. That being said, neither I, nor Nichathan Gaming owns, has affiliation to, or any form of control over Unity. All information in this walkthrough is subject to become obsolete at any moment and there are no guarantees that anything inside of this walkthrough will work. By continuing to follow this walkthrough, you understand that neither Johnathan Nichols nor Nichathan Gaming are responsible for whatever may happen. That being said, I put a lot of time and effort into this walkthrough and I sincerely hope that it can help you.
</br>**[Back To Top](#Table-of-Contents)**

### 1.2 Details
This walkthrough was typed by Johnathan Nichols of [Nichathan Gaming](https://play.google.com/store/apps/dev?id=5505294983591200024) on May 14th 2024. The walkthroughs purpose is to supplement the lack of documentation by Unity which claims that it is impossible to apply a Shader created with Shader Graph to an element on a Canvas with the render mode set to screen space overlay.
</br>**[Back To Top](#Table-of-Contents)**

### 1.3 Before continuing you should have
- [The Unity Hub](https://unity.com/download).
- A LTS [Unity Editor](https://unity.com/download) version 2022.3.5f1 or later. **This solution should work with previous and later versions of Unity but layouts may change**
</br>**[Back To Top](#Table-of-Contents)**

## 2 Instructions
### 2.1 Issue Discussion 
The issue with adding a material that is of a *Shader Graph* type to a *Canvas* with a *render mode* set to *screen space : overlay* is that the *Shader Graph* is not rendered and you will only see a large black rectangle in the place of your UI element. This is because of how Unity exports their *Shader* files for *Shader Graphs*. We overcome this issue by copying and pasting the *Shader* code that Unity generates and removing a few sections that end up causing *Shader Graph* files to not function on the *Canvas*.

### 2.2 The Guide Was Too Long, And I Did Not Want To Read It All
The simple solution to this problem is to create a functioning *Shader Graph* using a 2D *Sprite Renderer* for testing. Then you view the generated shader and copy the entire contents to an empty *Shader* file. Next, you want to remove all but the first *Pass* block and then remove the *Tags* block from the first *Pass*. The resulting code will work perfectly fine on any element in a *Canvas* with a *render mode* set to *screen space : overlay*.

### 2.3 Scene Setup
<br/>In this guide, I used 2 different **Sprite (2D and UI)** images to demonstrate that it works. Any image file that you have will work just fine if you wish to follow allong. You may even use no image or default Unity images.
<br/>Start with a blank scene which contains a **Main Camera**, an **EventSystem**, a **Sprite Renderer** (with a scale set to 0.2f, 0.2f, 0.2f so it may display on the Game window nicely), a **Canvas** (with a Render Mode set to Screen Space - Overlay), and an **Image** (set as a child of the **Canvas**)
| Hierarchy            | Canvas            | Canvas Image            | Sprite Renderer |
|:-------------------------:|:-------------------------:|:-------------------------:|:-------------------------:|
|![Hierarchy](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/efd25eab-7f00-427b-8e5b-ebedb953a431)| ![Canvas](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/d1f9e862-f1f8-4c7b-8e98-c2c66dd922f9) | ![CanvasImage](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/a762d3a5-7d5c-492f-9724-4ed01f78fb4d) | ![SpriteRenderer](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/7aa297ba-58fb-4e42-b067-737176da659f)|

### 2.4 Unity Editor Setup
<br/>To continue, you must have **Shader Graph** installed. **[See Steps](#Steps)**

#### 2.4.1 Steps
<br/>2.4.1.1 Open the **Package Manager**.
<br/>2.4.1.2 Go to the **Unity Registry** Packages tab.
<br/>2.4.1.3 Scroll down to **Shader Graph**. Ensure that it is installed or install it.

| 1 | 2 | 3 |
|:---:|:---:|:---:|
|![Package Manager](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/338250a8-f019-4c53-b069-97c66fd4ae50)|![Unity Registry](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/20b26594-e01d-411d-aa2d-bda69b7fd265)|![Shader Graph](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/31b322c0-c91a-41ee-beda-44fe90e059b5)|

### 2.5 Create A Shader Graph
<br/>2.5.1 Create a **Shader Graph**. 
<table>
  <tr>
    <th>Inner Steps</th>
    <th>Visual Guide</th>
  </tr>
  <tr>
    <td>
      <table>
        <tr><td>Right-click in the <i>Project/Assets</i> or navigate to <i>assets</i></td></tr>
        <tr><td>Go to <i>Create</i></td></tr>
        <tr><td>Go to <i>Shader Graph</i></td></tr>
        <tr><td>Go to <i>BuiltIn</i></td></tr>
        <tr><td>Go to <i>Unlit Shader Graph</i></td></tr>
      </table>
    </td>
    <td><img alt="Guide Image" src="https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/d44aa9a2-df7d-4eea-9e0b-635a04a211c7" /></td>
  </tr>
</table>
<br/>2.5.2 Create a <b>Material</b> from the <b>Shader Graph</b>
<table>
  <tr>
    <th>Inner Steps</th>
    <th>Visual Guide</th>
  </tr>
  <tr>
    <td>
      <table>
        <tr><td>Right-click on the <i>Shader Graph</i> in the <i>Project/Assets</i> folder</td></tr>
        <tr><td>Go to <i>Create</i></td></tr>
        <tr><td>Go to <i>Material</i></td></tr>
      </table>
    </td>
    <td><img alt="Guide Image" src="https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/7c52431f-0880-4e61-a87d-4d0bdf5d9f8e" /></td>
  </tr>
</table>
<br/>2.5.3 Apply the <i>Material</i> to the <i>Sprite Renderer</i> by dragging the <i>Material</i> from the <i>Project/Assets</i> folder onto the Image/Sprite Renderer/Material section. <i>This will allow us to see the changes made to our <b>Shader Graph</b> whenever we save it.</i>

![Visual Guide](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/ad641a43-dadb-4200-b65e-58f4118ebd56)
<br/>2.5.4 Open the *Shader Graph*.
![Untouched Shader Graph](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/70664fb0-1093-4332-91be-0ff334cdca5a)

### 2.6 Setting Up The Shader Graph
<br/>2.6.1 Create the parameters: MainTex (Texture2D) and Gradient (Gradient). *MainTex* must be spelled exactly as this parameter will capture the sprite attached to the **Image** and **Sprite Renderer**.
| MainTex | Gradient | End Result |
|:---:|:---:|:---:|
|![MainTex](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/0a424d4d-a756-43f2-8975-72576070787f)|![Gradient](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/56389934-e126-46c4-a597-5acf8bdc7f21)|![End Result](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/35c52f59-2e01-439d-85a8-b6fc8c88834c)|
<br/>**Note** : The next few steps will be to set up the **MainTex** section of the *Shader Graph*. To create a new *Node*, one may right click on an open section of the *Shader Graph* window or drag a line to an open section of the *Shader Graph*.
<br/>2.6.2 Drag the **MainTex** parameter onto the window.
<br/>2.6.3 Create a **Sample Texture 2D** and connect **MainTex** to the **Texture(T2)** input of the **Sample Texture 2D**.
<br/>2.6.4 Create a **Multiply** and connect the **RGBA(4)** of the **Sample Texture 2D** to the **A(4)** input of the **Multiply**.
<br/>2.6.5 Create a **Vertex Color** and connect the **Out(4)** of the **Vertex Color** to the **B(4)** input of the **Multiply**.
<br/>2.6.6 Create another **Multiply** and connect the **Out(4)** of the first **Multiply** to the **A(4)** input of the second **Multiply**.
<br/>**Note** : The next few steps will be to set up the **Gradient* section of the *Shader Graph*. This section is editable to fit the needs and wants of the **Shader**.
<br/>2.6.7 Drag the **Gradient** parameter onto the window. (Clicking on the **Gradient** parameter and then on the image to the right of the *Default* property in the **Graph Inspector** will allow one to set the **Gradient** values.)
<br/>2.6.8 Create a **Sample Gradient** and connect the **Gradient** to the **Gradient** input of the **Sample Gradient**.
<br/>2.6.9 Create a **UV**.
<br/>2.6.10 Create a **Split** and connect the **Out(4)** of the **UV** to the **In(4)** of the **Split**.
<br/>2.6.11 Connect the **R(1)** of the **Split** to the **Time(1)** of the **Sample Gradient**. (The gradient image should now be visible in the **Sample Gradient** dropdown. Also, one may see the outputs R(1), G(1), B(1), A(1). R-Horizontal Gradient, G-Vertical Gradient, B-Left Color, A-Right Color)
<br/>2.6.12 Create a **Multiply** and connect the **Out(4)** of the **Sample Gradient** to the **A(4)** and **B(4)** of the **Multiply**. (This will deepen the color of the gradient and make it closer to an actual gradient as the default *Shader* gradients are too soft.)
<br/>**Note** : The next few steps will combine steps 2-7 and 8-12 and make the **Sprite Graph** display on the **Sprite Renderer**.
<br/>2.6.13 Connect the **Out(4)** of the **Gradient's Multiply** (step 12) to the second **Multiply** (step 6) from the **MainTex** section. (This will add the color of the gradient to the image and color of the **Sprite Renderer** and **UI Image**.)
<br/>2.6.14 Create a **Split**.
<br/>2.6.15 Connect the **Out(4)** of step 6's **Multiply** to the **In(4)** of the **Split**. (This allows us to get the *Alpha* value from the color.
<br/>2.6.16 Connect the **Out(4)** of step 6's **Multiply** to the **Base COlor(3)** of the **Fragment**.
<br/>2.6.17 Connect the **A(1)** of the **Split** to the **Alpha(1)** of the **Fragment**.
<br/>2.6.18 Everything is all connected. Click **Save Asset** in the top left of the *Shader Graph* window to apply the changes and see them in the **Sprite Renderer**.
<br/>**Note** : One may notice that while the **Sprite Renderer** is currently displaying the **Shader** correctly, the **UI Image** will just be a black rectangle.

### 2.7 Converting A Shader Graph Into A Shader
<br/>This section will detail the last few steps needed to take the **Shader Graph** code generated by Unity and convert it into a **Shader** which can be applied to **UI Elements** on a **Canvas** with a *render mode* set to *screen space : overlay*.
<br/>2.7.1 Create a new **C# Script** and name it **CanvasGradient.Shader**. (CanvasGradient can be replaced with any name one wants however the file type must be *.shader*.)
