## Session Timeout

Before that, we must know how long we should keep the Session data

<img width="581" alt="Screenshot 2024-06-19 at 7 05 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8d26195b-53ce-4658-b217-ac65000cc334">
<img width="665" alt="Screenshot 2024-06-19 at 7 08 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c9987707-dc30-44c8-a14a-c869685986ec">

We can use Session Timeout.
- In web.xml:

  <img width="750" alt="Screenshot 2024-06-19 at 7 09 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7eeaefcf-40b7-477e-bfd7-d383020a431f">

- Programmatically:

  <img width="1014" alt="Screenshot 2024-06-19 at 7 11 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5273139a-dbf3-40a6-adf3-720991594a7e">
  <img width="1059" alt="Screenshot 2024-06-19 at 7 10 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0186361d-e12a-4cf1-a03e-f40ac26ec9bb">

# Session using Spring's annotation - @SessionAttributes

It stores the object that are supposed to be stored in the Session and run the whole process and use HttpSession behind the scene to store
our objects.

Suppose we want to store UserInfoDTO object, as it has userName, we can use it with SessionAttributes.

<img width="981" alt="Screenshot 2024-06-19 at 7 22 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/52bb6f96-f81f-4091-bc38-cc74b47b3553">

Whenever Spring would put data in UserInfoDTO, it would put the same inside Session. Hence, that object would be there in HttpSession.
This is counfigurable though(if we dont want to save it to HttpSession but Database). It should be noted that we can only store 
ModelAttributes/Model objects inside the Session attribute.

<img width="1058" alt="Screenshot 2024-06-19 at 7 22 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/69d2470e-39f2-42a2-bac6-836fd3333c64">
<img width="981" alt="Screenshot 2024-06-19 at 7 22 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4c1daf91-1fc5-48e4-bd52-3a4887f41988">
<img width="1060" alt="Screenshot 2024-06-19 at 7 24 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0ce85d1f-0cbc-42cb-a025-ff88de86d6af">

Now, if we want to use the same anywhere, we can use it.

<img width="876" alt="Screenshot 2024-06-19 at 7 25 56 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e3a785ba-aff2-41da-a20d-c944de187ec2">
<img width="960" alt="Screenshot 2024-06-19 at 7 26 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fc03034b-2895-44ee-a531-78a7c0a034b7">

But, we would come across an error

<img width="1229" alt="Screenshot 2024-06-19 at 7 28 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4f981c30-64d2-47c8-9912-806cf3c50aa9">

**Why so?**

This is because @SessionAttributes doesn't work with @ModelAttribute. We can use Model instead and manually add "userInfo".

Run the Application

<img width="689" alt="Screenshot 2024-06-19 at 7 37 52 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d116af19-e1ed-4261-bfad-55ffa8fd2392">
<img width="808" alt="Screenshot 2024-06-19 at 7 39 13 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/319565d9-9a03-464f-a1ea-4c84f0f5990f">

Stores userName and populates it this time

<img width="909" alt="Screenshot 2024-06-19 at 7 38 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8ab72b54-5095-4a00-ba35-fe81dde46d15">
<img width="815" alt="Screenshot 2024-06-19 at 7 38 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a406eff5-856d-4c25-87d2-6a892526c424">

*Note*

<img width="946" alt="Screenshot 2024-06-19 at 7 41 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3e264e56-72dd-4f96-9962-cbfd0ddff136">
<img width="1017" alt="Screenshot 2024-06-19 at 7 42 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6e51e183-1b54-4793-b52f-73b1fce4cff3">

## SessionAttributes - Unravelling the Mystery

<img width="971" alt="Screenshot 2024-06-19 at 7 49 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d294c643-6991-491a-a314-b4ff0bd78032">

Suppose we hit a url and Request goes to the Server. The Server handles the Request and then sends Response back. The time utilized for the same
is called as Request Scope.

<img width="988" alt="Screenshot 2024-06-19 at 7 52 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8bf2893e-c17f-4a62-99cd-4a1ccce5a69f">

Model object is part of Request Scope as it is created once the Request is sent to the Server.

<img width="521" alt="Screenshot 2024-06-19 at 7 55 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6edc8115-26b9-4a52-991e-aa3eb614ac8e">
<img width="1122" alt="Screenshot 2024-06-19 at 7 56 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d20d7a93-718b-49f1-bd01-0abe9baf1150">

Once we get the Response, this object is destroyed from the Request Scope.

<img width="823" alt="Screenshot 2024-06-19 at 7 58 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5c6070ca-2f8e-4bb8-be25-081a5442b663">

Consider the following,

<img width="606" alt="Screenshot 2024-06-19 at 7 59 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/157a4513-0f69-48ca-ae0e-b33a6c5a7767">
<img width="365" alt="Screenshot 2024-06-19 at 7 59 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cb436f05-5108-4cc1-943d-c9222b9dd909">

Suppose we create another Handler method and try to access the previous attributes, we won't be able to do so. This is because the Model and 
its attributes were part of previous Request scope when we hit "/first". Once the jsp page/Response is rendered, Request Scope gets over.
Next time when we hit "/second", that is considered as a new Request Scope and older Model attributes won't be available.

<img width="729" alt="Screenshot 2024-06-19 at 8 01 13 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cd3b6edf-2373-4943-9be0-84351335e454">

Now suppose we add it to SessionAttributes. This means the object will be persisted into the Session.

<img width="519" alt="Screenshot 2024-06-19 at 8 16 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b9adef56-54d8-4b15-8a45-e99d2d1d39eb">
<img width="1138" alt="Screenshot 2024-06-19 at 8 17 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ae14eecf-7cb5-49fd-bfd0-861c12db6be3">

Once the Request Scope is over, "Object1" would be destroyed. However, "Object1" in Session Scope will be persisted and will be available to
all the Controllers.

Consider another example,

<img width="1147" alt="Screenshot 2024-06-19 at 9 07 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/78c9191a-5d86-4895-bbb8-a348afc6b3ee">

## Implementation

<img width="699" alt="Screenshot 2024-06-19 at 9 11 22 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3ff2da78-6639-488b-9640-d0f301d080ea">
<img width="832" alt="Screenshot 2024-06-19 at 9 11 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f8f92320-da6b-4681-bfe9-cc597d9e0b71">

**Whenever the second url is hit, as the handler method exists in the same Controller, inside the Request Scope itself, "firstName" is pushed
to the Request Scope(as a Model attribute) from Session Scope.**

<img width="819" alt="Screenshot 2024-06-19 at 9 33 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2696243f-bc38-4f5c-b501-21fe194903ee">
<img width="409" alt="Screenshot 2024-06-19 at 9 12 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/94bba3cf-37c7-4aca-94fc-f9d765bd57d1">

**When we try to print firstName in jsp, where is it getting the value from? Model in Request Scope or Session Scope?**

- Whenever an object is available in both Request and Session scope, first priority is given to Request Scope.

  <img width="1145" alt="Screenshot 2024-06-19 at 9 37 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/15a2422b-ecda-4b5a-8eb3-8363eda4b60d">

- If it is not available in Request Scope, it gets it from Session Scope.

<img width="1180" alt="Screenshot 2024-06-19 at 9 38 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2dc1ccdd-d4ac-497f-b57a-27a4d4e6047a">

Fetching***

<img width="1089" alt="Screenshot 2024-06-19 at 9 40 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3095ad7d-f578-430d-b07c-fd1072854c4e">

*Note: "requestScope" and "sessionscope" is provided by jsp*

"firstName" is available in both Request and Session scope

<img width="915" alt="Screenshot 2024-06-19 at 9 42 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8f182b0a-af5b-476e-86dd-84b7aae7e812">

To get from Model,

<img width="753" alt="Screenshot 2024-06-19 at 9 50 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9be5b5d3-873a-4ec2-bce9-ebef1067a6e7">
<img width="651" alt="Screenshot 2024-06-19 at 9 50 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8d0ff8da-d8a9-4c90-a274-0590ed655a31">

**But do we really need to explicitely add it to the Model?**

<img width="1102" alt="Screenshot 2024-06-19 at 9 52 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9d70a32c-5638-40de-8ef8-6aac43b07fbc">

It's not necessary. We are already getting it from the Model which hints us that it is already available and need to require to be explicitely
added.

<img width="1054" alt="Screenshot 2024-06-19 at 9 54 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9b044234-3669-49b7-b5e8-e51c597770bb">

#### Example:

<img width="808" alt="Screenshot 2024-06-19 at 9 59 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8338ef4b-2246-4137-ba0b-cc08588660cd">

## Conversational Scope

<img width="975" alt="Screenshot 2024-06-19 at 10 32 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/236aea56-dc8f-4a09-a485-e9a81a388868">

@SessionAttributes is designed to provide a feature called "Conversational Scope". Spring provides Developer the ability to begin and end the 
scope. Developer can decide the scope based on their requirement.

We can use "SessionStatus" to remove th eobject from Session scope.

<img width="779" alt="Screenshot 2024-06-19 at 10 42 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/103a23e4-093f-416f-b1eb-b5da581466fa">

#### Can we use Session Attributes in a different Controller?

Spring Doc is confusing related to SessionAttributes. It suggests to restrict it to speicific handlers. For permanent Session Attributes,
it suggests to use Tradiditional "HttpSession.setAttributes()" instead.

<img width="1144" alt="Screenshot 2024-06-19 at 10 53 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b1c3f12d-7b47-4474-a937-c7e23d945d9a">

Let's try to use SessionAttributes in a different Controller.

<img width="1144" alt="Screenshot 2024-06-19 at 11 00 49 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4bd684fd-6670-4cca-a1d9-d4339ad72d3c">
<img width="365" alt="Screenshot 2024-06-19 at 11 00 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4b6f2155-02e9-449a-95ad-d916545c1ff7">

Spring MVC won't push object from Request Scope in the Second Controller as the Session Attribute is not associated with this Controller.
Also, @SessionAttributes is designed to have a conversational scope limited to *One* Controller.

#### But is there any other way to access the object present in Session Attributes?

- Yes using *@SessionAttribute*

  <img width="799" alt="Screenshot 2024-06-19 at 11 18 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/48d609ac-ce8c-4a19-b10b-d72b1adabbf2">
  <img width="823" alt="Screenshot 2024-06-19 at 11 21 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/55a911e8-ba7a-427f-926f-c0bd559ba482">
  <img width="501" alt="Screenshot 2024-06-19 at 11 22 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c24e6a8f-4b73-427a-a79b-ed57b8cdd8ba">
  
- However, Spring MVC won't push the object automatically in the Model. So we cannot get the attribute directly from Model
  scope

  <img width="771" alt="Screenshot 2024-06-19 at 11 10 37 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0f38f431-1e0c-487b-bbfa-072b63218f11">
  <img width="586" alt="Screenshot 2024-06-19 at 11 12 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4aa25517-41cc-44fe-b9b4-31c0d7d1fb63">
  <img width="828" alt="Screenshot 2024-06-19 at 11 13 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b06ea1f0-a9e6-41fe-8375-b2eeeb617221">
  <img width="1118" alt="Screenshot 2024-06-19 at 11 15 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fafbd6c8-2bf5-4b5f-ae4c-8d81987f57a9">

- But it is advised not to use Session Attribute in a different Controller: This is because if Session is cleared using     
  setComplete in original Controller, in a different Controller, where Session attribute might have been used will now return null.

  <img width="818" alt="Screenshot 2024-06-19 at 1 05 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2f21cd35-03da-43f7-8190-67c1bcacb0af">

  ## HttpSession VS SessionAttribute

  - HttpSession:

    <img width="754" alt="Screenshot 2024-06-19 at 1 14 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b669818c-9204-4629-9a04-d141c696bb16">
    <img width="767" alt="Screenshot 2024-06-19 at 1 15 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1be4e422-4e89-4cfa-9558-25dd92444bc4">
    <img width="810" alt="Screenshot 2024-06-19 at 1 17 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7acf74cb-e287-40e5-8cd0-1dd60e9f2dd3">

    Removing objects from HttpSessions -

    <img width="797" alt="Screenshot 2024-06-19 at 1 30 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1cb0fb45-78f4-4f6a-90ca-dedea9fcc4c5">
    <img width="803" alt="Screenshot 2024-06-19 at 1 32 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/136aeeea-84bd-4dab-9e1c-0f9ba21acb03">

  - SessionAttribute:

    Will we get Session value if we clear session(HttpSession) using setComplete? - Whatever is there in Session attribute will be removed
    but what has been added to HttpSession won't be removed. This is because with HttpSession we can add wide range of objects but with
    @SessionAttributes, we can only add Model objects.

    <img width="762" alt="Screenshot 2024-06-19 at 1 22 11 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0b9fedd9-656d-4ed1-8a6d-4ed30a5f1835">
    <img width="564" alt="Screenshot 2024-06-19 at 1 23 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/70b107c1-d79e-4223-8e1e-d42912949817">
    <img width="775" alt="Screenshot 2024-06-19 at 1 27 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ed68b3ac-17b2-406e-b3dc-b45908333820">
