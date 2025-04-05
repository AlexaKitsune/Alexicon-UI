
<template>
  <main class="AlexiconUi-MAIN display">

    <AlexiconComponent :type="'mainpage'">
      <AlexiconComponent :type="'searchbar'" :placeholder="'Search'" @get-switch-menu="(val) => menuActive = val"></AlexiconComponent>
      <div class="Alexicon-container">
        <AlexiconComponent :type="'asidemenu'" :active="menuActive" :size="200"></AlexiconComponent>
        <main class="Alexicon-main">
          
          <AlexiconComponent :type="'universalloginregister'"/>
          <AlexiconComponent :type="'text'" :placeholder="'hola'" :val="'hola'" @get-val="(val) => getValue(val, 'txt')"/>
          <AlexiconComponent :type="'text'" :placeholder="'hola'" :val="'hola'" :disabled="true"/>
          <AlexiconComponent :type="'button'">Button</AlexiconComponent>
          <AlexiconComponent :type="'button'" :disabled="true">Button</AlexiconComponent>
          <AlexiconComponent :type="'range'" :step="1" :min="6" :max="12"/>
          <AlexiconComponent :type="'range'" :val="25"/>
          <AlexiconComponent :type="'range'" :disabled="true"/>
          <div style="width: 50vw; height:400px ;"><AlexiconComponent :type="'textarea'" @get-val="(val) => getValue(val, 'textarea')" :resize="true"/></div>
          <br>.<br>
          <AlexiconComponent :type="'checkbox'"/>
          <AlexiconComponent :type="'checkbox'" :checked="true"/>
          <AlexiconComponent :type="'checkbox'" :disabled="true"/>
          <AlexiconComponent :type="'checkbox'" :disabled="true" :checked="true"/>
          <AlexiconComponent :type="'radio'"/>
          <AlexiconComponent :type="'radio'" :checked="true"/>
          <AlexiconComponent :type="'radio'" :disabled="true"/>
          <AlexiconComponent :type="'radio'" :disabled="true" :checked="true"/>
          <AlexiconComponent :type="'switch'" @get-val="(val) => getValue(val, 'switch')"/>
          <AlexiconComponent :type="'switch'" :checked="true" @get-val="(val) => getValue(val, 'switch')"/>
          <AlexiconComponent :type="'switch'" :disabled="true" @get-val="(val) => getValue(val, 'switch')"/>
          <AlexiconComponent :type="'switch'" :disabled="true" :checked="true" @get-val="(val) => getValue(val, 'switch')"/>
          <AlexiconComponent :type="'color'" :val="'#0f00f0'"/>
          <div><AlexiconComponent :type="'color'" :val="'#0f00f0'" :standalone="true"/></div>
          <div style="width:100px;"><AlexiconComponent :type="'knob'"/></div>
          <div style="width:100px;"><AlexiconComponent :type="'knob'" :val="45"/></div>
          <div style="width:100px;"><AlexiconComponent :type="'knob'" :disabled="true"/></div>
          <div style="width:30px;"><AlexiconComponent :type="'microknob'"/></div>
          <div style="width:50vw;">
            <AlexiconComponent :type="'video'" :src="require('../assets/video-cyberpunk.mp4')" :subtitles="testSubtitles"/>
          </div>
          <AlexiconComponent :type="'code'" :val="testCode.trim()"/>
          <AlexiconComponent :type="'markdown'" :val="testMd"/>
          <AlexiconComponent :type="'window'" :title="false">
            <button>Ejemplo de boton 123 456</button>
          </AlexiconComponent>
          <AlexiconComponent :type="'window'" :initialPosition="[100, 10]" :title="'Window'">
            <button>Ejemplo de boton abc def</button>
          </AlexiconComponent>
          <AlexiconComponent :type="'doc'" :src="'https://ia800903.us.archive.org/33/items/KanjiParaRecordar/Kanji%20Para%20Recordar.pdf'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/locacion.docx'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/onelife.xlsx'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/carnival.psd'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/LazenbyCompSmooth.ttf'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/example.html'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/example.htm'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/example.xml'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="'/examples/asPlain.csv'"/>
          <br>.<br>
          <AlexiconComponent :type="'doc'" :src="require('../assets/video-cyberpunk.mp4')"/>

        </main>
      </div>
    </AlexiconComponent>

  </main>
</template>

<script>
import AlexiconComponent from './AlexiconComponents/AlexiconComponent.vue';

export default {
  name: 'AlexiconUi',
  components: {
    AlexiconComponent,
  },
  data(){
    return{
      menuActive: false,
      testSubtitles: `
1
00:00:04,720 --> 00:00:06,720
One Two Three Four

2
00:00:07,119 --> 00:00:11,731
I couldn't wait for you to 
come and clear the cupboard

3
00:00:15,369 --> 00:00:19,000
But now you're gone and leaving nothing but a sign

4
00:00:23,208 --> 00:00:29,834
Another evening I'll be sitting reading in between your lines

5
00:00:30,888 --> 00:00:33,615
Because I miss you all the time

6
00:00:36,867 --> 00:00:38,723
So, get away

7
00:00:38,723 --> 00:00:43,144
Another way to feel what you didn't want yourself to know

8
00:00:43,144 --> 00:00:45,208
And let yourself go

9
00:00:46,249 --> 00:00:49,319
You know you didn't lose your self-control

10
00:00:50,304 --> 00:00:53,011
Let's start at the rainbow

11
00:00:53,011 --> 00:00:54,278
Turn away

12
00:00:54,278 --> 00:00:58,557
Another way to be where you didn't want yourself to go

13
00:00:58,557 --> 00:01:00,982
And let yourself go

14
00:01:01,496 --> 00:01:05,345
Is that a compromise?

15
00:01:06,786 --> 00:01:10,769
So, what do you wanna do, what's your point of view?

16
00:01:10,769 --> 00:01:14,466
There's a party, screw it, do you wanna go?

17
00:01:14,794 --> 00:01:18,485
A handshake with you, what's your point of view?

18
00:01:18,485 --> 00:01:21,954
I'm on top of you, I don't wanna go

19
00:01:21,954 --> 00:01:25,437
'Cause I really wanna stay at your house

20
00:01:26,007 --> 00:01:29,376
And I hope it all works out 

21
00:01:29,376 --> 00:01:32,843
But you know how much you broke me apart

22
00:01:32,843 --> 00:01:35,770
I'm done with you, I'm ignoring you

23
00:01:35,770 --> 00:01:38,055
I don't wanna know

24
00:01:38,939 --> 00:01:46,748
[ Music ]

25
00:01:47,619 --> 00:01:51,000
And I'm aware that you were lying in the gutter

26
00:01:55,283 --> 00:01:58,582
'Cause I did everything to be there by your side-ide

27
00:02:03,000 --> 00:02:09,562
So when you tell me I'm the reason, I just can't believe the lies

28
00:02:10,661 --> 00:02:13,745
And why do I still wanna call you

29
00:02:15,951 --> 00:02:19,969
So, what do you wanna do, what's your point of view?

30
00:02:19,969 --> 00:02:23,738
There's a party, screw it, do you wanna go?

31
00:02:23,923 --> 00:02:27,635
A handshake with you, what's your point of view?

32
00:02:27,635 --> 00:02:31,216
I'm on top of you, I don't wanna go

33
00:02:31,216 --> 00:02:34,728
'Cause I really wanna stay at your house

34
00:02:35,042 --> 00:02:38,483
And I hope it all works out

35
00:02:38,772 --> 00:02:41,786
But you know how much you broke me apart

36
00:02:41,786 --> 00:02:44,941
I'm done with you, I'm ignoring you

37
00:02:44,941 --> 00:02:47,498
I don't wanna know

38
00:02:47,911 --> 00:02:57,115
[Music]

39
00:02:57,248 --> 00:03:00,375
I don't know why I'm no one

40
00:03:02,613 --> 00:03:04,835
So, get away

41
00:03:04,835 --> 00:03:09,000
Another way to feel what you didn't want yourself to know

42
00:03:09,000 --> 00:03:11,184
And let yourself go

43
00:03:12,140 --> 00:03:15,153
You know you didn't lose your self-control

44
00:03:16,251 --> 00:03:18,993
Let's start at the rainbow

45
00:03:18,993 --> 00:03:20,237
Turn away

46
00:03:20,237 --> 00:03:24,620
Another way to be where you didn't want yourself to go

47
00:03:24,620 --> 00:03:26,777
And let yourself go

48
00:03:27,576 --> 00:03:31,302
Is that a compromise?

49
00:03:36,639 --> 00:03:40,535
So what do you wanna do, what's your point of view?

50
00:03:40,535 --> 00:03:44,489
There's a party, screw it, do you wanna go?

51
00:03:44,489 --> 00:03:48,229
A handshake with you, what's your point of view?

52
00:03:48,229 --> 00:03:51,741
I'm on top of you, I don't wanna go

53
00:03:51,741 --> 00:03:55,410
'Cause I really wanna stay at your house

54
00:03:55,752 --> 00:03:59,050
And I hope it all works out

55
00:03:59,278 --> 00:04:02,405
But you know how much you broke me apart

56
00:04:02,405 --> 00:04:05,273
I'm done with you, I'm ignoring you

57
00:04:05,273 --> 00:04:07,116
I don't wanna know

58
00:04:10,393 --> 00:04:33,375
[ Thanks for watching ]
      `,
      testCode: `
@font-face {
  font-family: Chunkfive; src: url('Chunkfive.otf');
}

body, .usertext {
  color: #F0F0F0; background: #600;
  font-family: Chunkfive, sans;
  --heading-1: 30px/32px Helvetica, sans-serif;
}

@import url(print.css);
@media print {
  a[href^=http]::after {
    content: attr(href)
  }
}
            `,
      testMd: `
# Marked in Node.js\n\nRendered by **marked**.
- **Preview:**  A live display of the generated HTML as it would render in a browser.
- **Lexer Data:**  What [marked] uses internally, in case you like gory stuff like this.
___

---

***
# h1 Heading 8-)
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading

## Emphasis

**This is bold text**

__This is bold text__

*This is italic text*

_This is italic text_

~~Strikethrough~~


> Blockquotes can also be nested...
>> ...by using additional greater-than signs right next to each other...
> > > ...or with spaces between arrows.

## Tables

| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

Right aligned columns

| Option | Description |
| ------:| -----------:|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

katex: $$c = \\pm\\sqrt{a^2 + b^2}$$

\`inline micro code\` and so on

こんにちは、私はアレクサです。
二十七歳です。
メキシコ人です。

\`\`\`css
@font-face {
  font-family: Chunkfive; src: url('Chunkfive.otf');
}
\`\`\`

\`\`\`js
const a = 1;
console.log("hola");
\`\`\`

Ready to start writing?  Either start changing stuff on the left or
[clear everything](/demo/?text=) with a simple click.

[Marked]: https://github.com/markedjs/marked/
      `,
    }
  },
  methods: {
    getValue(val, orig){
      console.log("getting value:", val, orig)
    }
  }
}
</script>

<style>
.AlexiconUi-MAIN{
  display: flex;
  flex-direction: column;
  background-color: light-dark(white, rgb(30, 30, 30));
}
</style>

<!--
Descripción del proyecto.

Todos los componentes contarán con un prop sizeMode="", el cual sólo recibirá dos valores: 'auto' y 'default' (el default será 'default').
  - auto: El elemento se ajustara al alto y ancho de su contenedor;
  - deault: El elemento solamente tendrá su tamaño predeterminado (en px);

Los componentes tendrán esta estructura:
  <AlexiconComp
    :type=""
    :sizeMode="" (opcional)
    @value="function()" (la función deberá capturar el valor)
  />

Componentes planeados:
  AlexiconText
  AlexiconButton
  AlexiconRange
  AlexiconCheckbox
  AlexiconRadio
  AlexiconColor

  AlexiconKnob
  AlexiconProgressBar
  AlexiconVideo
-->