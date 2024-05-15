# Unity-Shader-Graph-With-Canvas-Overlay
This repository will give detailed instructions on how to apply a *Shader* created with the *Shader Graph* window to an element on a *Canvas* with the *render mode* set to *screen space : overlay*. This repository will also be used as a supplement for the [YouTube video](https://youtu.be/n77mW90Dr8g).

## Table Of Contents
1. **[Initial Setup and Details](#1-Initial-Setup-and-Details)**
   1. **[Disclaimer](#1.1-Disclaimer)**
   2. **[Details](#1.2-Details)**
   3. **[Before continuing you should have](#1.3-Before-continuing-you-should-have)**
2. **[Instructions](#2-Instructions)**


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

![Final Solution](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/df6eaf98-9b68-4a64-bd18-cfb258251be3)

### 2.3 Scene Setup
<br/>In this guide, I used 2 different **Sprite (2D and UI)** images to demonstrate that it works. Any image file that you have will work just fine if you wish to follow allong. You may even use no image or default Unity images.
<br/>Start with a blank scene which contains a **Main Camera**, an **EventSystem**, a **Sprite Renderer** (with a scale set to 0.2f, 0.2f, 0.2f so it may display on the Game window nicely), a **Canvas** (with a Render Mode set to Screen Space - Overlay), and an **Image** (set as a child of the **Canvas**)
| Hierarchy            | Canvas            | Canvas Image            | Sprite Renderer |
|:-------------------------:|:-------------------------:|:-------------------------:|:-------------------------:|
|![Hierarchy](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/efd25eab-7f00-427b-8e5b-ebedb953a431)| ![Canvas](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/d1f9e862-f1f8-4c7b-8e98-c2c66dd922f9) | ![CanvasImage](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/a762d3a5-7d5c-492f-9724-4ed01f78fb4d) | ![SpriteRenderer](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/7aa297ba-58fb-4e42-b067-737176da659f)|

### 2.4 Unity Editor Setup
<br/>To continue, you must have **Shader Graph** installed.
<br/>2.4.1 Open the **Package Manager**.
<br/>2.4.2 Go to the **Unity Registry** Packages tab.
<br/>2.4.3 Scroll down to **Shader Graph**. Ensure that it is installed or install it.

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

![MainTex](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/d940c5a2-9e44-482d-9b9c-3c156766f3e9)

<br/>2.6.3 Create a **Sample Texture 2D** and connect **MainTex** to the **Texture(T2)** input of the **Sample Texture 2D**.

![Sample Texture 2D](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/74bbc163-db6f-4a17-a659-d72ef2ccfbc7)

<br/>2.6.4 Create a **Multiply** and connect the **RGBA(4)** of the **Sample Texture 2D** to the **A(4)** input of the **Multiply**.

![Multiply](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/b5633d77-b386-40d6-9389-f8dacb911149)

<br/>2.6.5 Create a **Vertex Color** and connect the **Out(4)** of the **Vertex Color** to the **B(4)** input of the **Multiply**. (The **Vertex Color** captures the **Color** parameter of the **Sprite Renderer** or **Image** that the material with this shader is applied to.)

![Vertex Color](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/51f34f81-64cc-4e7f-8329-416fc348ee77)

<br/>2.6.6 Create another **Multiply** and connect the **Out(4)** of the first **Multiply** to the **A(4)** input of the second **Multiply**.

![Second Multiply](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/dc8dfc3f-3bb4-43b4-a039-f081834c6210)

<br/>**Note** : The next few steps will be to set up the **Gradient* section of the *Shader Graph*. This section is editable to fit the needs and wants of the **Shader**.
<br/>2.6.7 Drag the **Gradient** parameter onto the window. (Clicking on the **Gradient** parameter and then on the image to the right of the *Default* property in the **Graph Inspector** will allow one to set the **Gradient** values.)

![Gradient](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/e31471f8-3ef2-4feb-bace-bd7d96b40c6c)

<br/>2.6.8 Create a **Sample Gradient** and connect the **Gradient** to the **Gradient** input of the **Sample Gradient**.

![Sample Gradient](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/08cf5bb6-9b99-4df7-b941-13182edaae10)

<br/>2.6.9 Create a **UV**.

![UV](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/bc605cda-6efb-4265-bb48-861554a9f23e)

<br/>2.6.10 Create a **Split** and connect the **Out(4)** of the **UV** to the **In(4)** of the **Split**.

![Split](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/610347ff-8bb6-4aa6-bab7-36a4e64330e7)

<br/>2.6.11 Connect the **R(1)** of the **Split** to the **Time(1)** of the **Sample Gradient**. (The gradient image should now be visible in the **Sample Gradient** dropdown. Also, one may see the outputs R(1), G(1), B(1), A(1). R-Horizontal Gradient, G-Vertical Gradient, B-Left Color, A-Right Color)

![Split SampleGradient Connection](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/3a382a4f-4b39-4268-8edc-92cd2afb69b4)

|Horizontal Gradient|Vertical Gradient|Left Color|Right Color|
|---|---|---|---|
|![Horizontal Gradient](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/355f8f35-eb0e-4283-bc1d-56c763af39bd)|![Vertical Gradient](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/b170d1ce-c5ed-4420-bd61-ff2c266fe746)|![Left Color](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/470be860-7f52-479e-9282-27d005b1813a)|![Right Color](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/a77496c6-3c43-46a4-84fe-19d26534399e)|

<br/>2.6.12 Create a **Multiply** and connect the **Out(4)** of the **Sample Gradient** to the **A(4)** and **B(4)** of the **Multiply**. (This will deepen the color of the gradient and make it closer to an actual gradient as the default *Shader* gradients are too soft.)

![Gradient Multiply](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/b2da3f89-f3c5-442c-883c-139077859178)

<br/>**Note** : The next few steps will combine steps 2-7 and 8-12 and make the **Sprite Graph** display on the **Sprite Renderer**.
<br/>2.6.13 Connect the **Out(4)** of the **Gradient's Multiply** (step 12) to the second **Multiply** (step 6) from the **MainTex** section. (This will add the color of the gradient to the image and color of the **Sprite Renderer** and **UI Image**.)

![Connecting the Multiplies](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/e6636801-b2e0-4554-b7a2-9a22e3e7c15d)

<br/>2.6.14 Create a **Split** and connect the **Out(4)** of step 6's **Multiply** to the **In(4)** of the **Split**. (This allows us to get the *Alpha* value from the color.)

![Split](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/45d07c6d-df83-4ef7-85d2-10743857f215)

<br/>2.6.15 Connect the **Out(4)** of step 6's **Multiply** to the **Base Color(3)** of the **Fragment**.

![Base Color](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/d90cc4a2-2f33-49c1-93ec-28f861f7b22f)

<br/>2.6.16 In the **Graph Inspector**, in the **Graph Settings** tab, change the **Built-In** **Surface Type** from **Opaque** to **Transparent**. (The parameter *Blending Mode* should be automatically added and set to *Alpha*.)

![Graph Settings](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/dc304841-4cfa-426a-ae8a-1bd699675965)

<br/>2.6.17 Connect the **A(1)** of the **Split** to the **Alpha(1)** of the **Fragment**.

![Alpha Connection](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/7518a8fd-32fc-4801-8036-f88ea7beb39a)

<br/>2.6.18 Everything is all connected. Click **Save Asset** in the top left of the *Shader Graph* window to apply the changes and see them in the **Sprite Renderer**. (Pressing `Ctrl+s` does not save a **Shader Graph** file.)

![Save Button](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/34f0feaa-05b0-4bec-8bbf-8dd3202428cd)

|Unsaved File|Saved File|
|---|---|
|![Unsaved](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/36c0828b-2892-4010-b958-162772952476)|![Saved](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/cf4602ff-a4d5-47c6-96fb-930217146692)|

<br/>**Note** : One may notice that while the **Sprite Renderer** is currently displaying the **Shader** correctly, the **UI Image** will just be a black rectangle.

|Sprite Renderer|UI Image|
|---|---|
|![Sprite Renderer](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/b318ba43-696b-4a81-a49b-dc0a09c19e24)|![UI Image](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/39cb3744-02ec-4c88-ba0b-228d08b92388)|

### 2.7 Converting A Shader Graph Into A Shader
<br/>This section will detail the last few steps needed to take the **Shader Graph** code generated by Unity and convert it into a **Shader** which can be applied to **UI Elements** on a **Canvas** with a *render mode* set to *screen space : overlay*.
<br/>2.7.1 Create a new **Unlit Shader**. (Create -> Shader -> Unlit Shader)

![New Shader](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/02aeb79e-0040-439d-95f3-ee33715e94d4)

<br/>2.7.2 Select the **Shader Graph** that you want to convert into a **Shader** in the *Project/Assets* window. Then click *View Generated Shader* in the *Inspector*.

![View Generated Shader](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/19d51c55-cefd-48cd-b41b-04a7bf83842d)

<br/>2.7.3 Return to the Unity Editor and open the **Unlit Shader** file from step 2.7.1. Then delete all of the contents within. (You should now have the *Generated Shader* and *Unlit Shader* files open in your text editor.)

![Open Files](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/345f9c20-e90a-40b6-b755-8cd3717ebd72)

#### 2.7.4 Describing The Parts Of A Shader
<br/>This sub-section will talk about the parts in a **Shader** as created by the Unity **Shader Graph**.
<br/>2.7.4.1 The first part of a **Shader** will be the *File Name*. This name will be how you find your **Shader** when you apply it to a **Material**. `Shader "Folder/File Name"`
<br/>**Note** : A **Shader** must have a file name but it can have between no folders to many folders. Using or not using folders for your shaders can be an effective way to keep your **Shaders** organized.

|No Folder|One Folder|Many Folders|
|---|---|---|
|![No Folder Name](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/f6945f72-4d13-4779-8a24-2e1cb0491912)![No Folder Material](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/84fb28d6-a374-43bc-910a-9189088ac337)|![One Folder Name](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/07366bef-f185-45fa-9867-4d79802b64c1)![One Folder Outer](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/a5eb68b3-e08a-4021-bc34-f17493a8f8d8)![One Folder Material](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/ee4d885a-d5db-43a4-8085-e928e1a8f865)|![Many Folders Name](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/daf2f656-0abf-4df1-bc4f-e749c11a327f)![Many Folders Outer](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/00a08ef2-88a2-433f-a44f-6e84d3919216)![Many Folders Inner](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/ffc36711-0fdc-44e6-9b16-c056f3ba5a74)![Many Folders Material](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/e85abe9c-b2ea-4a5d-b885-8c362b2747b6)|

<br/>2.7.4.2 The second part of a **Shader** will be the *Properties*. This is where we see *MainTex*, without these properties you may receive errors.

![Properties](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/78f1f288-f802-496d-bd36-0c2b9d5fa4d9)

<br/>2.7.4.3 The third part of a **Shader** will be the *SubShader*. This will hold the *Tags* and *Pass* sections of the **Shader**.

![SubShader](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/12a22db7-3f3a-450f-ae0e-cae3cae4f9fa)

<br/>2.7.4.4 The *SubShader* will have *Tags*. These should not be touched as they help describe how the **Shader** is displayed.

![Tags](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/1f6b0ffa-d7b5-4ccf-bee0-914da9dc2bda)


<br/>2.7.4.5 The final part of a **Shader** will be the *Pass* sections. These sections detail how exactly to display and handle the **Shader** and they are also why the **Shader Graph** does not work on a *Canvas* with the *render mode* set to *screen space : overlay*. (A *Pass* begins with `Pass {` and ends with `ENDHLSL }`.)
<br/>**Note** : Aside from the file name, this is the only part of the generated shader that we should edit.

![Pass](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/fced406a-1241-4127-a13e-dac6582fae4f)

<br/>2.7.5 Copy everything from the *Generated Shader* file from `Shader "FolderName/FileName"` to the end of the very first *Pass* `ENDHLSL }`. (When you copy this over, you should add 2 more curly brackets `}` to close off the **Shader**.)

|Start|End|
|---|---|
|![Start](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/f96c9afc-dfc8-4b2c-9232-610062553c36)|![End](https://github.com/Nichathan-Gaming/Unity-Shader-Graph-With-Canvas-Overlay/assets/103794085/79a3a507-a767-4c7e-b8e9-c236076c815b)|
















