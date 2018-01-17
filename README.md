# Typescript tips

## Callbacks and `this` context

So, you have callbacks that need `this` to be the class, right? Say no more.

From Javascript:

```js
  $scope.$on('partyStarts', self.playCaribeMix1997);
```

To typescript:

```ts
  // AVOID

  public musicPlaying: bool;
  
  private playCaribeMix1997() { 
    this.musicPlaying = true; // This will raise an error, cannot read musicPlaying of undefined.
  }
  
  this.$scope.$on('partyStarts', this.playCaribeMix1997); // IMPORTANT LINE: This doesnt preserve `this`.
  
  
  // DO

  public musicPlaying: bool;
  
  private playCaribeMix1997() { 
    this.musicPlaying = true; // This will raise an error, cannot read musicPlaying of undefined.
  }
  
  this.$scope.$on('partyStarts', () => this.playCaribeMix1997()); // IMPORTANT LINE: Arrow function wrapping allows preserving `this`
  
```
