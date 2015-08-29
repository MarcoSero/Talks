# Hi

---

## Marco Sero

### @marcosero

---

![](resources/ballmer.gif)
#[fit] Microsoft

---

![](resources/yammer-hackday.jpg)
#  
#  
#  
# [fit] iOS @ Yammer

---

![](resources/iphone.jpg)
# [fit] WORKING ON A
# [fit] LEGACY APP

---


# [fit] DEFINITION OF
# [fit] LEGACY

---

![](resources/legacy.jpg)
> "Anything *handed down from the past*, as from an ancestor or predecessor"

---

![](resources/floppy.jpg)
> "Obsolete"

---

# [fit] DEFINITION OF
# [fit] LEGACY CODE

---

![](resources/rage.jpg)

# [fit] No Unit Tests

---

![](resources/house_fire.jpg)

# Still used in
# [fit] Production

---

![right](resources/pisa.jpg)
# IT JUST WORKS*
##### *most of the time

--- 

![fit](resources/brontosaurus_outline.png)

# Written in a language that you don't typically do __new__ development in

--- 

![](resources/swift.jpg)
# Swift 1.2

---

![](resources/prehistoric-art.jpg)

# Old and complicated
# [fit] History

---

![](resources/kids.jpg)

# Many 
# [fit] Contributors...

---

![](resources/quit.gif)

# [fit] ...That have all quit

--- 

## Let's recap

:heavy_check_mark: Still used in production :boom:

:heavy_check_mark: Old or deprecated language :fire:

:heavy_check_mark: Without unit tests :scream:

:heavy_check_mark: Old history with many, many contributors... :family:

:heavy_check_mark: ...most of which not around anymore :runner:

--- 


![](resources/engineer-house-cards.jpg)

# Or whenever
# you feel like this

---

![](resources/party.jpg)
# [fit] Not much
# [fit] Legacy
# [fit] on iOS

---

![](resources/party.jpg)
## iOS development is new(ish) <br><br><br>
## Short app lifetime <br><br><br>
## Easier to re-write

---

# So why bother?

---

![fit](resources/yammer-stats.jpg)

---

![fit](resources/bad-code-bad.jpg)

---

![fill](resources/stopcomplaining.jpg)
# [fit] JUST
# [fit] STOP
# [fit] PLEASE
# [fit] STOP

---

![](resources/urlo.jpg)

# <br><br><br> WHERE DO I
# START?

---

#[fit] STATS

---

# Identify the risk and start there

```bash
$ find YourApp -iname "*.h" | 
    xargs grep -h 'interface' | 
    cut -d ' ' -f 2 | 
    while read class; 
    do echo `grep -r "\b$class\b" YourApp --include "*.m" | wc -l` $class; 
    done | 
    sort -n -u
```

> from *Destroy All Software* screencasts. 

---

![fit](resources/risk-pipe-output.jpg)

---

![](resources/git.png)

# [fit] Leverage
# [fit] git

--- 

![](resources/xcode.png)

# [fit] Git Blame 
# [fit] ⌥⌘⇧⏎

--- 

![fit](resources/loading.png)

--- 

![fit](resources/xcode-crash.png)

--- 

![fit](resources/xcode-blame.jpg)

---

# [fit] git log -L 1,1:/your/file

---

![fill](resources/linus.jpg)
#  
#  
#  
# [fit] COMMIT MESSAGES

--- 

![fit](resources/bad-commits.jpg)

---

![fit](resources/bad-commits.jpg)
![fit](resources/better-commits.jpg)

---

## Your 
# [fit] COMMIT MESSAGES 
## are your
# [fit] LEGACY 

---

![fill](resources/dead.jpg)
# [fit] \(Maybe\) DEAD
# [fit] CODE

---

![left](resources/tombstone.jpg)
# [fit] TOMBSTONES

```objectivec
- (void)possibleDeadCode
{
    // current date when tombstone was added
    log_tombstone(@"2015-08-21"); 
}
```

- Log found?
    :arrow_right: Code is alive :raising_hand:
- Log not found?
    :arrow_right: Code is dead :skull:

<br>

> From David Schnepper's Ignite talk, "Isn't That Code Dead?"

---

![fill](resources/destruction.jpg)
#  CONTINUOUS
# [fit] DESTRUCTION

---

![](resources/inheritance.jpg)

# [fit] Inheritance

---

![inline fit](resources/subclasses-bad.jpg)

---

```objectivec
@implementation RootViewController
- (void)doSomething:(NSString *)aString {  }
@end

@implementation RootViewController_iPad
- (void)doSomething:(NSString *)aString {
    NSLog(@"%@ iPad", aString); 
}
@end

@implementation RootViewController_iPhone
- (void)doSomething:(NSString *)aString {
    NSLog(@"%@ iPhone", aString);
}
@end

RootViewController *vc = [[RootViewController_iPad alloc] init];
[vc doSomething:@"cool"]; // prints "cool iPad"
```

---

```objectivec
@implementation RootViewController
- (void)doSomething:(NSString *)aString {  }
@end

@implementation RootViewController_iPad
- (void)doSomething {
    NSLog(@"iPad"); 
}
@end

@implementation RootViewController_iPhone
- (void)doSomething:(NSString *)aString {
    NSLog(@"%@ iPhone", aString);
}
@end

RootViewController *vc = [[RootViewController_iPad alloc] init];
[vc doSomething:@"cool"]; // prints nothing
```

---

```swift
class RootViewController: UIViewController {
    func doSomething(aString: String) {  }
}
class RootViewController_iPad: RootViewController {
    override func doSomething(aString: String) {
        print(aString + "iPad")
    }
}
class RootViewController_iPhone: RootViewController {
    override func doSomething(aString: String) {
        print(aString + "iPhone")
    }
}
```

---

```swift
class RootViewController: UIViewController {
    func doSomething(aString: String) {  }
}
class RootViewController_iPad: RootViewController {
    override func doSomething() { // COMPILE ERROR
        print("iPad")
    }
}
class RootViewController_iPhone: RootViewController {
    override func doSomething(aString: String) {
        print(aString + "iPhone")
    }
}
```

---

![right](resources/chris.jpg)
> *"I've got your back"*
-- Chris Lattner on Swift's Safety

---

#[fit] THIRD-PARTY
#[fit] DEPENDENCIES

--- 

![](resources/dependencies.jpg)
# [fit] AVOID
# [fit] THEM
### (if possible)

---

<br>
<br>
> *Build a small, but non-trivial, Rails app. [...] Go away for six months. Come back and update all of your dependencies. Your app no longer works.*
<br>
-- Gary Bernhardt

---

<br>
<br>
> *Build a small, but non-trivial, iOS app. [...] Go away for six months. Come back and update all of your dependencies. Your app no longer works.*
<br>
-- Marco Sero

---

![](resources/facepalm.jpg)
#  
#  
#  
# [fit] FORKS

---

## Recap:

- Start identifying the risk
- Leverage Git
- Spend some time writing good commit messages
- Continuous destruction of dead code
- Avoid subclasses and touch them with care
- Third party dependencies have a cost and private forks are almost always a bad idea

---

![fit](resources/techical-debt.jpg)

--- -

![](resources/good-citizens.jpg)
# [fit] BE A GOOD CITIZEN

---

# HAVE FUN
# :smile::laughing::joy:

---

## Thank you.<br>

## @marcosero<br>

- *Working Effectively with Legacy Code* by **Michael Feathers**
- *Utter Disregard for Git Commit History* by **Zach Holman**
    http://zachholman.com/posts/git-commit-history/
- *Destroy All Software screencast* by **Gary Bernhardt**
    https://www.destroyallsoftware.com/screencasts
- *Isn't That Code Dead?* by **David Schnepper**
    https://www.youtube.com/watch?v=29UXzfQWOhQ

