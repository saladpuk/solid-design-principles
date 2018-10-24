@title[Cover]

@snap[north-west byline]
  @color[orange](S).O.L.I.D Principles Series
@snapend

@snap[west headline text-white]
  SRP  
  @size[0.6em](@color[orange](S)ingle-Responsibility Principle)
@snapend

---

@title[SRP Definition]

### Single-Responsibility Principle
> A class should have only one reason to change.  
-- Robert C. Martin (Uncle Bob)

@size[0.5em](If you can think of more than one motive for changing a class,)  
@size[0.5em](that class has more than one responsibility.)

---

### Example 01 - Rectangle class

```
public class Rectangle
{
    public void Draw()
    {
        // Draws the rectangle on the screen.
    }

    public double GetArea()
    {
        // Computes the area of the rectangle.
    }
}
```

+++

### Example 01 - problems

![img](assets/img/srp/rectangle01.png)

+++

### Example 01 - Apply SRP

![img](assets/img/srp/rectangle02.png)

---

#### If a class has more than one responsibility

* Couple
* Fragile designs @color[orange](*- Code smell*)

---

### Single-Responsibility Principle
Another wording for the SRP is:
> Gather together the things that change for the same reasons. Separate those things that change for different reasons.  
-- Robert C. Martin (Uncle Bob)

---

#### Example 02 - Email class

```
public class Email
{
	public void SetSender(string sender) { ... }
	public void SetReceiver(string receiver) { ... }
	public void SetContent(string content) { ... }
}
```

@[3-4](Adding a new protocol will create the need to add code for parsing and serializing the content for each type of field.)
@[5](Adding a new content type (like html) make us to add code for each protocol implemented.)

+++

#### Example 02 - Email class (SRP)

```
public interface IContent 
{
	string GetContent();
}

public class Email
{
	public void SetSender(string sender) { ... }
	public void SetReceiver(string receiver) { ... }
	public void SetContent(IContent content) { ... }
}
```

@[1-4,10](Split the content responsibility. Adding a new type of content supported causes changes only in Content class.)
@[8-9](Adding a new protocol causes changes only in the Email class.)

---


### Misunderstanding

@color[red](@fa[times]) 1 Class = 1 Method

---

### Conclusion
The Single-Responsibility Principle is one of the simplest of the principles but @color[orange](one of te most difficult to get right). Conjoining responsibilities is something  that we do naturally. Finding and separating those responsibilities is much of what software design is really about.