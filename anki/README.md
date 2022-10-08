# Anki

This directory contains information on how I format my anki cards.

---

## Chimera Card

A chimera card that can be either a word/sentence. Note, I tag cards if they can be categorized. I explain this in the Anki section of the website of this repository. If a sentence/context is provided in the `context` field, it will be a sentence card. If a sentence/context is not present, it will be a word card:

```html
<div class="front">
  <!--Show context if context-->
  {{#context}} {{context}} {{/context}}
  <!--Show word if no context-->
  {{^context}} {{word}} {{/context}}
</div>
```

The front template I use is [chimeraFront.html](./chimeraFront.html).

The back template I use is [chimeraBack.html](./chimeraBack.html).

The fields I use are:

1. context
2. word
3. Back
4. POS
5. image
6. wordAudio
7. contextAudio

---

Vocab and sentence cards. Must include specifications as described below.

- Vocab/word cards - can include optional media and examples on back `[Front, Back]`.
- Sentence/context cards - can include optional media and examples on back `[Front (word within a sentence and word is bolded), Back]`.

Each card will contain data similar to how [ODict](https://github.com/TheOpenDictionary/odict) and [Wikipedia categorizes language](https://en.wiktionary.org/wiki/Wiktionary:Entry_layout) entries. This way we can have cards rich with contextual information. Tagging is also useful metadata for filtering (example: Duolingo, Pokemon, Trip to XYZ, Example Context).

**ODict Format**

```xml
<dictionary name="Example Dictionary 1">
  <entry term="run"> 
    <ety description="Latin root">
      <usage pos="v">
        <group description="A number of verb usages">
          <definition value="(vertebrates) To move swiftly">
            <example value="The dog ran after the cat." />
            <example value="The horse ran away." />
          </definition>
          <definition value="(fluids) To flow." />
          <definition value="(nautical, of a vessel) To sail before the wind, in distinction from reaching or sailing close-hauled." />
          <definition value="(social) To carry out an activity." />
          <definition value="To extend or persist, statically or dynamically, through space or time." />
          <definition value="(transitive) To execute or carry out a plan, procedure or program." />
        </group>
      </usage>
      <usage pos="n">
        <definition value="Act or instance of running, of moving rapidly using the feet." />
        <definition value="Act or instance of hurrying (to or from a place) (not necessarily by foot); dash or errand, trip." />
        <definition value="A pleasure trip." />
        <definition value="Flight, instance or period of fleeing." />
        <definition value="Migration (of fish)." />
        <definition value="A group of fish that migrate, or ascend a river for the purpose of spawning." />
      </usage>
    </ety>
  </entry>
  <entry term="dog">
    <ety description="Latin root">
      <usage pos="v">
        <definition value="a dog" />
      </usage>
    </ety>
  </entry>
  <entry term="cat">
    <ety description="Latin root">
      <usage pos="v">
        <definition value="a cat" />
      </usage>
    </ety>
  </entry>
</dictionary>
```

**Wiktionary Format**

```
==English==

===Noun===
{{en-noun}}

# A piece of [[furniture]] to [[sleep]] on.

===References===
* ''The Oxford Paperback Dictionary''
```

**Applying this to Anki Cards**

```json
{
  "specifications": [
    {
      "object": "front",
      "description": "The front of the Anki card (word or sentence)",
      "required": true
    },
    {
      "object": "back",
      "description": "The back of the Anki card (word/sentence translation)",
      "required": true
    },
    {
      "object": "part of speech",
      "description": "category of the syntactic behavior of the word",
      "required": true,
      "choices": [
        "noun",
        "verb",
        "adjective",
        "adverb",
        "pronoun",
        "preposition",
        "conjunction",
        "interjection",
        "determiner",
        "expression"
      ]
    },
    {
      "object": "image",
      "description": "image of the card",
      "required": false
    },
    {
      "object": "audio",
      "description": "example sentence and/or word audio",
      "required": false
    }
  ]
}
```

Language decks can be bilingual, monolingual, or both. Personally, I keep all objects in the specification above in my native language besides the front. Having images and audio (example sentence and or term) is preferable.

```json
{
  "cards": [
    {
      "front": "The dog's **bark** was very loud",
      "back": "**l'aboiement** du chien était très fort",
      "part of speech": "noun"
    },
    {
      "front": "The tree's **bark** was dark brown",
      "back": "**l'écorce** de l'arbre était brun foncé",
      "part of speech": "noun"
    }
  ]
}
```

---

**[Sentence Cards vs Vocab Cards: In-Depth Comparison](https://www.youtube.com/watch?v=GLfmKWhLhjk) Summary**

You can either have production or comprehension cards. Production cards try to get you to produce your target language in some way. Comprehension cards present you with the target language and you just have to understand its meaning.

Two examples of production cards: your native language on the front and the target language on the back, cloze cards where you have to fill in the blank of a target language sentence. 

Two examples of comprehension cards: given a vocab card in your target language understand the meaning of it in your native language, given a sentence in your target language understand it in your native language.

We’ll focus on comprehension cards. Of comprehension cards there can be 4 types: audio vocab/sentence cards and text vocab/sentence cards.

**Text Sentence Cards**

Goal is to understand the sentence as a whole

- front: sentence containing single unknown target word
- back: definition of sentence and unknown target word
- optional image
- optional audio of sentence and/or target word

**Text Vocab Cards**

Goal is to recall the and understand the word

- front: target word
- back: definition of word
- example sentence (to get a sense of what it means or how it’s used)
- optional image
- optional audio of sentence and/or target word

**Vocab/Sentence Card Comparison**

Vocab Card Pros

- easily understandable as a beginner
- only need the jist of example sentence

Vocab Card Cons

- no capability for polysemous words
- not great for abstract definitions of complex words (would be better to have context to start with)

Sentence Card Pros

- capability for polysemous words
- good for abstraction definitions of complex words

Sentence Card Cons

- exhausting as a beginner
- difficult for beginners

There are words that have a one-to-many relationship with meaning (polysemous). This is a major shortcoming of vocab cards: the ambiguity of words. For example, the word “bark” in english can be both a verb and a noun and have multiple meanings for each part of speech.

The word “bark” as a noun could mean the sound a dog makes or the outer layer of a tree. You could make two vocab cards for this but then there would be no way to tell which is which. The other option is to have a single vocab card with multiple meanings for that part of speech. But, this makes things stressful and not effective. The better option is to make multiple sentence cards.

The hybrid solution is an Anki card with a conditional word field. What the heck is this? Well this is a chimera that allows you to switch the cards type at any point in its life. If the word field is filled out, it turns into a word card. If the word field is empty it is a sentence card. The logic is like this:
