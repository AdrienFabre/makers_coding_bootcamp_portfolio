# Makers Coding Bootcamp Portfolio

This portfolio is under construction. This is a draft.

The [Makers Software Engineering Bootcamp](https://makers.tech/) is a 12 week, full-time, onsite course. Here is the portfolio that shows evidences of my learnings. The repositories shared in this document are not meant to be perfect but to show the progression in each of the topics listed in the Table of Contents below.  

---

## Table of Contents

  - [I can make anything](#i-can-make-anything)
    - [I can TDD anything](#i-can-tdd-anything)
    - [I can program fluently](#i-can-program-fluently)
    - [I can debug anything](#i-can-debug-anything)
    - [I can model anything](#i-can-model-anything)
    - [I can refactor anything](#i-can-refactor-anything)
    - [I have a methodical approach to solving problems](#i-have-a-methodical-approach-to-solving-problems)
  - [I help my teams succeed](#i-help-my-teams-succeed)
    - [I use an Agile product development process](#i-use-an-agile-product-development-process)
    - [I write code that is easy to change](#i-write-code-that-is-easy-to-change)
    - [I can justify the way I work in a business context](#i-can-justify-the-way-i-work-in-a-business-context)
    - [I can grow collaboratively](#i-can-grow-collaboratively)
  - [I am equipped for long term growth](#i-am-equipped-for-long-term-growth)
    - [I manage my own well-being](#i-manage-my-own-well-being)
    - [I can learn anything by myself](#i-can-learn-anything-by-myself)

---

## I can make anything

---

### I can TDD anything


TDD stands for Test Driven Development. It means that before writing any code, we think, plan and write the result that we want to obtain. We focus on the simpliest next step. We postpone decisions.

Once the next step is defined, we write and run the test. Then, we read the error messages produced by our test and fix them one by one. The error messages drive the development of our code, this is TDD.

````md
Example of an error message

NoMethodError:
       undefined method `prompt' for Echo:Class

````

Here the error message tells us to create a method called 'prompt'. But let's start at the beginning.

To be implemented correctly, the TDD has a process that is summarised in 3 steps: first, it is called RED, the test fails, second, GREEN, the test passes, third, REFACTOR, the code is improved. This is the basics.

Our challenge starts by defining a test from a requirement or a user story. A user story is usually framed this way:

````user story
User story

As a logged in user,
So I can buy a fruit online,
I want to add an apple to my basket.
````

Here, what is important is to select the keywords and to create a test from it. The test is going to impact the design of the code, this is important. We need to understand what the client wants and it may be worth asking for more details if the specifiations or user stories are not clear enough. Here is one possibility for the test.

````ruby
Feature test

context 'as a logged in user' do
  it 'adds an apple to his basket' do
    user_account = Account.new
    user_account.add_to_basket('apple')
    expect(user_account.basket).to include apple
  end
end
````

Here, in the test, first, we define the noun that is going to do the action (account) for 'logged in user', second we define the verb that is going to do the action (add_to_basket) and third, the noun that is going to be used during the action (apple). In that case, we are using [Rspec testing framework](http://rspec.info/) , this is for the programming language Ruby. Here we define 'user_account' as an instance of 'New Account', 'add_to_basket' as a 'method' with 'apple' as an 'argument'. Then we write the 'expectation', we expect the 'user_account' to have a 'basket' that includes an 'apple'.

A test is like a black box where we describe an input and an output that summarises a user story but that does not explain how it is going to be solved. A user story test is created from the user perspective, it is called a 'Feature Test', a non-software-developer person should be able to understand it. We can micmic a user interaction to help us.

Then we decompose the feature test that is often a complex black box into smaller, simplier black boxes that we call 'Unit Test'. Each time we encounter an error message from the feature test, we create a 'Unit Test' that is going to be simplier about the code but may be only readable by software-developers. The process is the following:

![feature-unit-test-cycle](readme_images/feature-unit-test-cycle.jpg)

Previous to the tests, from the specifications or users stories, I read and refine entirely the requirements to get a general understanding of the user interactions. The big picture helps me to get an idea of the direction. Then make a quick drawing of the entire project so I can easily keep it in mind. If I find it necessary, I write or rewrite the users stories so that they have a more manageable size to work with. I then order the user stories and create a diagram of the classes, properties and functions needed for the first feature, this is the planning part. Finally, I start the process:

Red phase - Test

- 1- I translate the first user story into my first feature test.
- 2- I run the test to make sure my feature test fails.
- 3- I write the failing unit test matching the feature test.
- 4- I run the test to make sure my unit test and feature test fail for the same reason.

Green phase - Implement

- 5- I write the easiest code to make the unit test pass, no more.
- 6- I run the tests and check if unit test passes. If not, repeat step 5.
- 7- I repeat steps 5-6 until the feature test passes entirely.

Refactor phase - Refactor

- 8- I modify the code without adding any feature. I make sure all best practices are respected.
- 9- I run tests again to check that the refactoring did not break the tests.
- 10- I then start the loop again with a new user story.

---

When I plan, I work on the scope of my test. Making my test simple but meaningful, one of the risk is to test the state instead of the behavior.

When I commit, I add, commit and push to [Github](https://github.com), is helps to save the different version of my work, working alone or in a group. I can also take more risk when I find new solution because a saved version of the working code exists.

After 15 minutes working on writing some code to implement a test, it is good to step back and wonder if the test we are doing is the good one in term of what we are testing and of how much we are testing, this is why it is recommended to remove all our changes since our last commit (revert) and simplify our test.

We can see how the 'Unit test' is defined by the 'Feature test error'. In the example taken earlier, the first error would be that we don't have a class Account.

````md
NameError:
     uninitialized constant Account
````

This is the moment to create a file for our unit test for our class 'Account', 'account_spec.rb'. Then, to answer this message error, we create an 'account.rb' file with.

````ruby
class Account

end
````

Because this test is very basic and simple, we tend to use it only to test the testing environment works and then to skip it. Also, the future test we will write will test this, and as we want to avoid redundant tests, we may delete previous tests in the refactor phase.

Keeping our example, then we are going to receive an error message because we don't have a method called 'add_to_basket'.

````md
NoMethodError:
       undefined method `add_to_basket' for #<Account:0x000055f7f162a400>
````

We can write the Unit Test sending the same error message.

````ruby
 it 'answers to add_to_basket' do
    user_account = Account.new
    expect(user_account).to respond_to(:add_to_basket)
  end

````

And here we solve the unit test problem, then we move to the next one.

````ruby
class Account do
  def add_to_basket

  end
end
````

Then we are going to receive an error message because 'add_to_basket' should receive an argument from the Feature Test.

````md

ArgumentError:
       wrong number of arguments (given 1, expected 0)

````

So we will create a new Unit Test and solve it this way.

````ruby
class Account do
  def add_to_basket(item)

  end
end
````

Then we would keep going this way, I am not going to go further here. What is important is to understand the step by step approach so we always know what to do next. And if we do hesitate because we work with a new testing framework we can search online, and we know what we are looking for.

Trying to do small steps we may be tempted to create unecessary test, for example, one usual mistake is to test State over Behavior. The previous example was testing the Behavior because 'add' is the name of the method that will transform the 'items'. However, the following test is a bad one because it tests the state.

````ruby
  it 'basket to have an apple' do
    user_account = Account.new
    expect(user_account.basket).to include('apple')
  end
````

Because to solve this test I could code the answer directly, this is called to 'hardocde'. So, I am testing a State I am writing, not a Behavior I am creating, this is why the following test is unecessary.

````ruby
it 'adds an apple to the basket' do
  class Account
  attr_reader :basket
  def initialize
  @basket = ['apple']
  end
end
````

Our approach to Test Drive Development is Behavior Driven Development.

I can Test Drive Develop anything means that when I am facing a problem, I am able to divide it in small chunks, that I am able to be very clear about what I want to achieve in that chunk, that I develop my solution step by step, writing the test first and then finding the solution. It means that whatever language or project I am working on, I am able to consistently use a methodology such as the Red-Green-Refactor, in other words, I can use a process to create structured code, easy to read, debug and update.

---

Here are few interesting examples. When we go further with testing we encounter several cases:

---

When a new class is created during unit test, we create a fake, here is an example:

````ruby

let(:plane) { Plane.new }

````

https://github.com/AdrienFabre/airport_challenge_ruby/blob/6a4b4bc5c3e53e515494e33da19f00478da84f63/spec/airport_spec.rb

In the Airport Challenge, in the Airport class unit test, so we can use an instance of the class Plane, we create a double that we can access everywhere in this test. This is a good way to make the Unit Test independent, so we only test the Airport class with the Airport Unit Test. While the feature test would test everything together, so we would never see a double in a feature test.

So we were able to use a plane in our tests for the Airport class while it was not existing yet.

---
When we want to test what is output in the terminal, we use the following syntax:

````ruby
  it "prompts the user to say something with 'Say something:'" do 
      expect { Echo.prompt }.to output('Say something:').to_stdout
  end
````

https://github.com/AdrienFabre/echo_ruby/blob/0307b636c4e105de552e64d75b369bb57daec184/spec/echo_spec.rb

This syntax enables us to create an expected output, that will not be returned at the end of the code, but like something that is displayed in the terminal and that a user can see.

---

When we want to test what is inputed in the termial, we use the following syntax:

````ruby
it 'receive the user answer' do
  allow(Echo).to receive(:gets).and_return('hello, world/n')
  expect(Echo.receive).to eq('hello, world')
end
````

https://github.com/AdrienFabre/echo_ruby/commit/48baaf4b5a212df450160a0ba9de9ec7bbeeb67a#diff-fb4dc7c0bd38dc2a980d90e370c3338a

This 'allow...' syntax enables to mimic the user input in that specific case because it is use on ':gets', however we can use it in many situation to fake the behavior of another class for example.

---

When we want to test a class that includes the time we need to fake it, in that case we can use:

````ruby
    time_now = Time.new(2019, 1, 2, 3, 4, 5, '+00:00')
    allow(Time).to receive(:now).and_return(time_now)

````

https://github.com/AdrienFabre/echo_ruby/blob/master/spec/echo_spec.rb

Here we are using one of the class defined by Ruby, the class Time.

---

Here what is interesting, in the Rock Paper Scissors game, is that we are faking randomness.

````ruby
    it 'returns a shape' do
      allow(Kernel).to receive(:rand).and_return(1)
      expect(Computer.new.shape).to eq 'Paper'
    end
````

https://github.com/AdrienFabre/rps-challenge/blob/master/spec/computer_spec.rb

Here we are using the class define by Ruby, Kernel to return a fix number, so we can expect a specific outcome.

---

When we want to do a feature test in a complete app, we don't want the user to use the terminal, but an interface through the browser, in that case we use feature tests mimicing the user interface. In this case we use Capybara testing framework to test the [Sinatra](http://sinatrarb.com/) and Ruby environment.

````ruby
feature 'display the celebration message' do
  scenario 'display the number of days before birthday date' do
    visit("/")
    fill_in :name, with: "Erin"
    select '26', from: 'day'
    select 'Jan', from: 'month'
    click_button "Submit"
    expect(page).to have_content "Your birthday will be in 1 day!"
  end
end
````

https://github.com/AdrienFabre/birthday_app/blob/334a29bc2c364e30420e98666e2b1c8b56303592/spec/features/display_birthday_spec.rb

Here the test is doing the job of testing for the sentence to be right, however, this sentence could be valid every month, while the ideal would be to have test that is valid once a year.

This feature test drived me to create those 2 unit tests that are testing the cases if it is my Birthday or if it is not.

````ruby
  it "return birthday if the date selected is today" do
    Time.stub(:now).and_return(Time.mktime(2019,1,25))
    day_selected = 25
    month_selected = 1
    expect(Calculator.new(day_selected,month_selected).time_left).to eq 'birthday'
  end

  it "return the number of days between now and the date selected" do
    Time.stub(:now).and_return(Time.mktime(2019,1,25))
    day_selected = 26
    month_selected = 1
    expect(Calculator.new(day_selected,month_selected).time_left).to eq 1
  end
````

https://github.com/AdrienFabre/birthday_app/blob/master/spec/calculator_spec.rb

---

Here is another example of the Airport Challenge, where I am using a new language, Javascript, and one of its [testing framework Jasmine](https://jasmine.github.io/2.0/introduction). Here I am creating a block, BeforeEach, that is going to happen before each test. In that case, I am creating a new Airport, the class I am testing. I am also creating a Plane, which is a way to create a fake Plane that is going to answer to the method 'land'.

````javascript

 beforeEach(function(){
    airport = new Airport();
    plane = jasmine.createSpy('plane',['land'])
  });

````

---

In the Makers Final Project, we used [React](https://reactjs.org/), so Javascript, to feature test our app tested with [Cypress](https://www.cypress.io/).

````cypress
it("can create a new card", () => {
    cy.get('#plus').click()
    cy.get("input[name=title]").type('Test Card');
    cy.get("input[name=urgent]").click();
    cy.get("#Create").click()
    cy.contains('Test Card');
  })
````

Here we did not succeed to properly Test Drive our application, we did create feature test after we created our app. We would have needed a some more time to be confortable enough with Jest and Enzyme to Test Drive the entire application. This is where I found the limit of learning a new language and test drive at the same time. In that moment, spiking is a way to learn, otherwise it is hard to test something that we don't know about.

---

Once everything is TDD, it brings several advantages.

Firstly, the test coverage is theoricaly 100%, with Ruby we used [Simplecov](https://github.com/colszowka/simplecov).

---

### I can program fluently

From my experiences with human languages, as a French that learnt English and Russian within the past 10 years, I would divide fluency in different parts.

The part that is similar among languages and that makes it easier to learn new languages such as the main logic, structures, rules, characters, environments all of this, even if it is not identical helps to understand and use new languages easily.

The part that is unique to a language such as syntax specificities and particular abilities, this is often what we mention when we describe a language, what is does differently than others. 

Programming language have those two parts too, learning Ruby was challenging because I did not have any reference from previous programming language. Once I understood the patterns, the big picture, the details, I acquired the key words to quickly search online whatever syntax was missing. Because I did not know the syntax but I knew what I was willing to use in term of logic or structure. And this first language helped me to explore Javascript and a little bit of Java with their own differences and similarities. Then, learning the test framework language was another step, because the logic was different, however after RSpec, Jasmine was also easier.

Program fluency means that I have explored enough programming languages so that I am confident that I can use my acquired abilities to understand program languages, to search efficiently and to learn quickly, new programming languages.

At the edge of programming fluency, there is on one side the ability to translate human language such as specification or user stories into code and to write code using the best practices such as Test Driven Development, Don’t Repeat Yourself, and Single Responsibility. In other words, keep in mind the person that may use your user interface and your code.

---

### I can debug anything

A bug is an unexpected behavior. Debugging is about finding why this behavior occurs and modifying it so it matches our expectations.
Being able to debug anything is about having a clear process to find the source of a bug, a process that can be used in any language. This process is divided in two main parts.

Getting visibility

Tighten the loop

Method 
Process

I get visibility, I print

I tighten the loop

Follow the flow

View Controller Model 
Browser 
Test results

Different languages 

Process

Bug from the console
Bug from the test
Bug from terminal 
Tighten the loop and get visibility in different languages

---

### I can model anything

Transforming specification and user stories into a few squares and arrows, that develops our understanding of the big picture and help us to define each part and how they fits together.

Wireframe

Diagram

Flow

Miro

Break down 

Link steps

Structure 

Logic 

Adapt

Properties and interactions 

---

### I can refactor anything

Knowing what is good and bad.

Single responsibility 

Redundancy DRY

RESTFul
https://en.wikipedia.org/wiki/Representational_state_transfer

---

### I have a methodical approach to solving problems


---

## I help my teams succeed

---

### I use an Agile product development process

XP 
Scrum Master
MVP 
Cycles 
Facilitation


 

Wiki

---

### I write code that is easy to change


---

### I can justify the way I work in a business context

I can communicate in a way that people understand why I am taking a decision and why it makes sense to me into a context of a developer in a professional environment. I take into account client's perspective and needs.


Engineering
Listening
Communicate

Client Understanding 

Understand problems

---

### I can grow collaboratively

I can evolve in a team where I contribute to my individual progress as well as the individual progress to every person in the group and to the collective goal.

Networking

Talks 

Ask 

Feedback 

Answer

Listening 
Explaining

Will 
Elliot 
Kim

---

## I am equipped for long term growth

---

### I manage my own well-being

Balance

Yoga 

Meditation 

Swimming

Blog

 Dana

---

### I can learn anything by myself

Motivation 
Focus 
Perseverance
Method 
Practice 
Wellbeing

Small town to Big cities.
Small business to Corporate.
Vocational Electronics to Business Engineering
Cook to Buyer.

Russian lanugage.

Facilitate events.

Wordpress.
http://attitude-michele-joel.com 
http://adrienfabre.net 

 Feedback

Rohan Metha from MakeSense (an open source volunteer-driven network creating events to support social entrepreneurs)

Very soon after attending his first event he was eager to jump on board and learn how to facilitate one of our workshops. By conducting these workshops he got to deeply understand several social entrepreneurs and help them figure out how to improve their business. He did these extremely well and soon became part of the core team. 6 months after he attended his first MakeSense workshop Adrien was the lead in organising a large-scale event “Food Glorious Food” tackling food waste with a full day event with workshops, activities, and talks featuring 12 different social entrepreneurs in the food sustainability sector. Adrien found the venue, negotiated using it for free, came up with the concept, created the marketing materials and was directing 6 other volunteers to pull off a really successful event.

Adrien demonstrates a really strong work ethic. If he says he will do something he will go to great lengths to make sure it gets done. I have also found that he learns very quickly. If he is interested in something he will dive head first into it, contacting people to talk to and create opportunities to learn as much as he can by doing. He is a self-starter and very good at finding ways to improve the ways we work together.





==== draft feedback list  ====

Dana
Katerina Georgiou
Ed 

Process Review  
Kai Hoffman
Brooke Wooley
Gabriel

William Dunk
Ibrahim Butt

Sherif Shendidy


Elliot Jennings on Acebook

Before working on Jungl-Book with Adrien I thought I had grasped the concept of agile development. It was the guidance of Adrien during this project which allowed our team to now say we are confident with the framework. He gave us workshops on the scrum process and was devoted to making us stick to the following agile development in our second week. He is driven to manage a project and it seems to be a natural position for him as he always focuses on the bigger picture even when the team are being slightly short-sighted.


Vaith Schmitz on Acebook

Adrien has been great to work with on JunglBook.
He's super eager to learn and always found a ton of resources for us to use to understand a topic. His curiosity led us to question our processes more and he was the driving force behind us deciding to redo everything from scratch in week 2 to follow strict agile principles. Especially in this implementing good practices, Adrien was a huge asset to the team by his knowledge and experience.


Krzysztof Balejko

I have worked with Adrien on several occasions, during our pair programming sessions he has proven to be very good at debugging, championing the process of tightening the loop and getting visibility. I’ve fond his code to be of very good quality therefore I had no problem in understanding the logic behind his code base.
Adrien starts each of his projects with careful planing and I was invited to join in before both bowling and front-end API challenges. During the process Adrien has demonstrated his abilities of modelling user interaction. We have used Realtime Board during both sessions for diagraming and general brainstorming. I would very happily work with him again!

Alice ( see details on google doc )

Overall. I think your process was good. But you may need to believe in it more. You asked a very good question to start, split the task into steps, and started writing one behaviour test to start. You reasearch process could use some more practice, but it's doing the job. You seem to know your tools.
If there is one thing to work on, it may be self-awareness. What are you doing. How can you see when/if you are stuck, or if you just need to give it more time.
