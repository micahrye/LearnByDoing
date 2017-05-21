# LearnByDoing

## Let’s Get Going! 
I thought it would be good to put our past work to work a bit during this week as we learn about the basics of debugging and navigation in React-Native (RN). We will work through this week’s learning by building a simple application and adding navigation to it. In the process we explore some tools and approaches to debugging.  

Like much of “computer science” debugging is part art form, part great tools. Good debugging skills will save you lots and lots and lots and lots (and lots) of time and frustration. 

A famous quote about debugging is, “Everyone knows that debugging is twice as hard as writing a program in the first place. So if you're as clever as you can be when you write it, how will you ever debug it?” (Brian Kernighan) 

Any seasoned programmer knows the value of good debugging tools and their own “best” practices. I will try and cover a few simple approaches with you and some of the tools that can be used with RN. 

Let’s start be creating a new RN app. 
```
$ react-native init LearnByDoing
$ cd LearnByDoing
$ atom ../LearnByDoing   <I use atom you can use your prefered editor>
```

Alright now let’s install a couple packages
```
$ npm install --save react-navigation
$ npm install --save react-native-animated-sprite
```
Good, now let's startup Genymotion (or other) and get your Android emulator running. Once your emulator is running start you new app. 
```
$ react-native run-android
```

You should see

<img src="https://raw.githubusercontent.com/micahrye/LearnByDoing/master/media/firstBuild.png" width="300" height="184">


Great, now open "index.android.js" and make the following changes.  
```
...
export default class LearnByDoing extends Component {
  constructor (props) {
    super(props);
    console.log("hum, why didn't I see this?")
  }
  
  componentWillMount () {
    console.warn("the component will mount");
  }
  
  componentDidMount () {
    console.error("the component did mount");
  }
  
  componentWillUnmount () {
    console.warn("say goodbye while you can");
  }
...
````

Now rebuild your app and you should see the following: 

<img src="https://raw.githubusercontent.com/micahrye/LearnByDoing/master/media/error.png" width="300" height="184">

By calling console.error RN will display a large red error modal with information about the error that. If you "dismiss" the error, or press anywhere on the screen, you will then see this: 

<img src="https://raw.githubusercontent.com/micahrye/LearnByDoing/master/media/warn.png" width="300" height="184">

The yellow notification bar along the botton indicatings a warning. While the use of console warn and error are not meant for debugging, per se, they can be used for quick debugging info that gets your attention. Generally speaking you would use console.warn moreso then error. 

You might be wondering why we did not see anything for "console.log()" Well warn and error are meant for user notification, i.e. the end user, while loging is somthing that is done for you not the end user. As a result console log does not have a UI display element like warn and error. 

With that said, console.log is a much hander way of doing "print statement" debugging. 

Let's change our class to look like this: 
```
export default class LearnByDoing extends Component {
  constructor (props) {
    super(props);
    console.log("I see I am in the constructor");
  }
  
  componentWillMount () {
    console.log("the component will mount");
  }
  
  componentDidMount () {
    console.log("the component did mount");
  }
  
  componentWillUnmount () {
    console.log("say goodbye while you can");
  }
  
  render() {
    console.log("this thing is going to render now")
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.android.js
        </Text>
        <Text style={styles.instructions}>
          Double tap R on your keyboard to reload,{'\n'}
          Shake or press menu button for dev menu
        </Text>
      </View>
    );
  }
}
```
