# NDCDevOpsWorkshop Wrap Up & Additional Resources

## Wrap-up & Feedback, and Resources

Thanks for spending the last two days with us. We hope you enjoyed the workshop and learned a lot!

## Recommendations

* Destroy your infrastructure using the Octopus Runbook, as you will continue being charged if you don't destroy your infrastructure.
* Keep Github Actions, as there should be no cost.
* Octopus Cloud will remain free for 30 days, or you can use the Octopus Community edition, which has up to 5 targets, five users with limited permissions, five projects, and 20 worker hours per month but is valid for 12 months and can be extended for free each year.
* Check out the [reading list](#ReadingList) I've pulled together to help you understand more about "Why should we adopt DevOps?"

## Octopus Deploy Resources

* [Octopus documentation](http://octopus.com/docs/).
* [Octopus Guides](https://octopus.com/docs/guides) where you can select your CI/CD pipeline to generate a video, documentation, and a TestDrive VM that walks you through a complete CI/CD setup.
* [Octopus YouTube channel](http://octopus.com/videos).
* [Octopus Events Page](https://octopus.com/events) for upcoming webinars and for previously recorded webinars.
* [Octopus Webinar instance](http://webinar.octopus.app/).
* [Sample Octopus instance](http://samples.octopus.app/).
* [Octopus Twitter](https://twitter.com/OctopusDeploy).

## Github Actions Resources

* [Microsoft Learn](https://docs.microsoft.com/en-us/learn/paths/automate-workflow-github-actions/) is a great Microsoft Learn course on Github Actions.
* [Understand Github Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)
* [Github Actions Marketplace](https://github.com/marketplace?type=actions)
* [Understanding Github Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)

## Azure Resources

* [Azure Docs](https://docs.microsoft.com/en-us/learn/azure/)
* [Azure Fundamentals Course](https://docs.microsoft.com/en-us/learn/paths/az-900-describe-cloud-concepts/)
* [Azure Training Days](https://www.microsoft.com/en-us/trainingdays/azure)

## Infrastructure as Code Resources

* [Azure Quickstart Templates](https://azure.microsoft.com/en-au/resources/templates/)
* [ARM Template Tutorial](https://docs.microsoft.com/en-gb/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell)
* [ARM Template best practises](https://docs.microsoft.com/en-gb/azure/azure-resource-manager/templates/best-practices)
* [Deploy and manage resources in Azure by ARM Module](https://docs.microsoft.com/en-us/learn/paths/deploy-manage-resource-manager-templates/)

Please let the Workshop leader know if you believe the workshop can be improved in any way. 

Please leave any feedback for the workshop [using our feedback form](https://oc.to/workshopfeedback)

## DevOps Reading List {ReadingList}

This is a cut-down version of a blog on the Octopus Deploy website, and you can read it in full [here](https://octopus.com/blog/devops-reading-list).

### 1. The Goal (Goldratt: 1984) {#goal}

The fact that this is by far the oldest book in my selection is a testament to how well it's aged and how important and timeless it is.

The Goal is a novel about Alex Rogo, a senior manager at UniCo, an auto-parts manufacturing company. Business is going badly. To avoid a massive restructuring program and many job losses, Rogo must simultaneously improve performance, quality, and profitability before a seemingly impossible deadline.

His initial efforts don't go well. He falls into various traps of old-fashioned plant management, focusing on local optimizations and cost-efficiencies. Fortunately, he bumps into Jonah, an eccentric old friend, who gives him some curious advice that contradicts everything he believed about effective plant management.

The Goal offers a genuinely engaging, personal, accessible, and practical approach to learning about fundamental lean principles like value streams, flow, waste, global efficiencies, and the theory of constraints.

Unlike the other books on the list, The Goal hardly references software. It is, after all, a book about manufacturing, not software development. This is a good thing since it helps the reader understand the foundational lean principles in their original context, which means the reader requires zero prior IT experience to appreciate the concepts.

If you'd like to learn more about how these lean principles can be applied to modern software development, I encourage you to read either [The Phoenix Project](#phoenix) (a modern retelling of The Goal, based in an IT department) or [Lean Software Development: An Agile Toolkit](#lean) (a more formal textbook).

For more reviews, as well as procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/113934.The_Goal)

### 2. Lean Software Development: An Agile Toolkit (Poppendieck, Poppendieck: 2003) {#lean}

A book that's stood up to the test of time.
  
I wouldn't like to guess how many software books have "Agile" in the title. Arguably, "Agile" was the original marketing buzzword for software.

I believe these buzzwords work so well for selling software, training, and certifications because they have a fundamental truth. These ideas make a lot of technical and commercial sense.

It may be mocked, but The Agile Manifesto had its place. For many, it was an important stepping stone toward articulating Agile. However, better articulation for Agile is Mary and Tom Poppendieck's "Lean Software Development: An Agile Toolkit," which came along two years later.

The Poppendiecks take 7 of the core lean principles and talk practically about how they translate from the manufacturing domain into software development:

1. Eliminate Waste
1. Amplify Learning
1. Decide as Late as Possible
1. Deliver as Fast as Possible
1. Empower the Team
1. Build Integrity In
1. See the Whole

Along the way, they cover 20 tools for applying the lean principles into practice, such as Value-Stream Mapping, working in iterations, and refactoring.

This book stands up as one of the (if not the) best articulation of what Agile is, how it builds on stable Lean foundations, and why specific practices result in better software delivery outcomes. As an "Agile" book, it's not technically a "DevOps" book (it was written six years before Patrick DeBois accidentally gave us *that* buzzword). Still, this book was an essential chapter in the genesis of DevOps.

For those who want to learn more about Lean principles in their original manufacturing context, check out [The Goal](#goal). For those who would like to know how these Agile ideas have evolved with the emergence of DevOps, take a look at [The DevOps Handbook](#handbook). For those who want to go deeper into software design/architecture, try [Domain-Driven Design: Distilled](#ddd). Finally, for those who are more interested in the human side of Agile/DevOps, you might prefer [The Five Dysfunctions of a Team](#dysfunc) (more personal) or [Team Topologies](#tt) (more strategic).

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/194338.Lean_Software_Development)

### 3. Domain-Driven Design Distilled (Vernon: 2016)  {#ddd}

Domain-Driven Design (DDD) is an approach that enables folks to create loosely coupled architectures and avoid creating a "big ball of mud" monolithic system, which is painful to develop, deploy, or maintain. <a href= "https://martinfowler.com/bliki/DomainDrivenDesign.html">Martin Fowler does a better job of describing it on his blog</a> than I can reasonably expect to achieve in a few paragraphs here.

Central to DDD is the idea of "Bounded Contexts," which can be used to define the scope of any one part of the system. Team members acknowledge that the language used in any context is consistent but might also vary between different contexts. This allows teams to focus on solving the correct problems in the right places and establishing appropriate interfaces between different contexts to avoid complicated dependencies and introducing mistakes due to subtle contextual differences. [Again, Fowler does a great job of explaining Bounded Contexts in more detail here.](https://martinfowler.com/bliki/BoundedContext.html)

Most folks recommended [Eric Evans' Domain-Driven Design](https://www.goodreads.com/book/show/179133.Domain_Driven_Design), but Matthew Skelton (author of [Team Topologies](#tt)) also recommended Vernon's "distilled" edition to me. After a little research, I learned that the Evans book has excellent reviews and is recognized as the gold standard for DDD. However, it's also perceived as long and complicated. (It's 560 pages long and costs over $50, making it longer and more expensive than any of the other books in this post.)

Since this was my first book about DDD, I purchased a copy of Vernon's "distilled" edition instead. Half the price and only 130 diagram-rich pages. I've included the Vernon book in my list because I'm uncomfortable recommending a book I haven't read, but I recognize that many readers may prefer to go straight for the Evans book.

The Vernon book is an excellent primer on DDD, and it's relatively easy to digest by anyone with little software development experience. It's especially relevant for anyone struggling with a monolithic system at the moment or who would like to avoid their stuff gradually turning into one.

After reading Domain-Driven Design Distilled, you might like to go deeper on DDD with the Evans book mentioned above. Alternatively, you might want to read more about how loosely coupled architectures are so much easier to work with. This is covered to some extent in both [Accelerate](#accelerate) and [The DevOps Handbook](#handbook). 

You might also like to take a look at [Sam Newman's Building Microservices](https://www.goodreads.com/book/show/22512931-building-microservices) (which narrowly missed a spot in this post) and in [Site Reliability Engineering](#sre) you learn how Google maintains a large, complicated environment with many loosely coupled services.

Finally, I encourage you to look at [Team Topologies](#tt). Software architecture starts with team architecture, and Team Topologies uses Conway's Law to apply the ideas of bounded contexts and loosely coupled systems to the way we architect the teams in our IT departments. 

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/28602719-domain-driven-design-distilled)

### 4. Continuous Delivery (Humble, Farley: 2011)  {#cd}

This book formalized many ideas about deployment pipelines that have since become ubiquitous. It details some technical details about Config as Code, builds and deployment automation, and effective testing strategies.

Most folks don't tend to read this book end to end. (It's pretty dry and technical.) Instead, it's best used as a reference book. If you intend to adopt new technological practices, it's worth reading the associated chapter before you get started to help you understand how to approach it.

The book is generally pretty technical, mainly focusing on the practical implementation of deployment pipelines. However, it also discusses hand-offs, rapid iterations, experimentation, and learning. In many ways, it becomes difficult to differentiate between CD and DevOps once you start to see CD through this broader lens.

Today, there is some confusion about the scope of CD. For some, it's simply about the practical implementation of deployment pipelines. For others, CD encompasses broader cultural and organizational issues. Some would go as far as to say that DevOps is part of CD rather than the other way around.

For example, the two authors seem to be on opposite sides of this debate. Jez Humble went on to co-author [Accelerate](#accelerate), which has the word "DevOps" on the front cover and describes a set of "Continuous Delivery" capabilities that are distinct from other capabilities under the headings "Architecture," "Product and Process," "Lean Management and Monitoring", and "Cultural". At the same time, Dave Farley views CD as a synonym for DevOps (and in the past, he claimed that DevOps was but a component of CD), as [he expressed on his YouTube channel](https://www.youtube.com/watch?v=MnyvgFDh-kw&list=PLwLLcwQlnXBw9jv5tFXQC_ch-VCXwPikM&index=4). 

If you enjoyed Continuous Delivery, you might also enjoy [Site Reliability Engineering](#sre). It's a similar technical book, designed for huge IT departments, that covers many additional topics from production/operations/maintenance. On the other hand, if you found CD a little dry and would like something more accessible, try [The DevOps Handbook](#handbook) or [Accelerate](#accelerate) instead.

For more reviews, as well as procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/8686650-continuous-delivery)

### 5. The Five Dysfunctions of a Team (Lencioni: 2002) {#dysfunc}

Andrew Clay Shafer's "wall of confusion" slide at Velocity in 2009 struck a chord because it was an excellent articulation of the "core chronic conflict" between dev and ops. It resonated. Painfully.

Most large organizations have more complex political structures than simply "dev" and "ops," and it's a struggle to get all functions working in alignment – yet this is precisely what's required to achieve short lead times, frequent releases, and "flow."

Alignment is only possible with teamwork, and teamwork is not possible without well-trained team players. As Gerald Weinberg famously said, "no matter what they tell you, it's always a people problem".

The DevOps community has always been intensely focused on people and culture. However, tech folks are generally far more comfortable talking about software or automation than talking about emotions, trust, or personal vulnerabilities. This leads to one of DevOps' problems: Too often, it's boiled down to automated deployments, infrastructure as code, or the latest vendor tool. These over-simplifications entirely miss the point.

The Five Dysfunctions of a Team provides a logical framework for addressing "the people problem". The first 180 pages tell a "Leadership Fable", similar to [The Goal](#goal), [The Phoenix Project](#phoenix), or [The Unicorn Project](#unicorn). DecisionTech is a start-up with all the raw ingredients for success, but the senior leadership team is a dysfunctional mess. Kathryn Peterson, the new CEO, is tasked with uniting these individually brilliant but wily and guarded individuals to turn the company's fortunes around.

The final 40 pages review the framework Kathryn uses to create an effective team. You could skip the fable and just read these 40 pages and be done in an hour, but that would be like reading sheet music in silence or learning to use some new tech by reading the documentation without ever installing it. To be truly appreciated, it's valuable to read the fable and observe the framework in action.

If your most significant problems are "people problems", this book should be one of the first that you read.

After reading "dysfunctions," if you'd like to learn how to structure multiple teams in your organization for success, you might want to try reading [Team Topologies](#tt). If you fancy another fable, take a look at [The Phoenix Project](#phoenix), in which some of the exercises from "dysfunctions" are used to bring together warring leadership teams amid a project management disaster. 

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/21343.The_Five_Dysfunctions_of_a_Team)

### 6. The Phoenix Project (Kim, Behr, Spafford: 2013)  {#phoenix}

The Phoenix Project is a satire of every company you've ever worked for. It's full of the larger-than-life characters that you often worked with in the past. There's the grumpy DBA, the lone engineer who understands how all the most critical systems work, the senior leadership characters who don't understand tech and many others. You read this book and recognize your colleagues. One by one, you giggle to yourself. There's Dave. That's Susan. Oh, wait – that's me.

Gene Kim was so inspired when he read [The Goal](#goal) that he wanted to retell it in the context of software development. The Phoenix Project is an homage. Alex Rogo is replaced by Bill Palmer, a middle manager who's just been _unwittingly_ promoted into a senior leadership role after his predecessor was fired. He works for Parts Unlimited, another auto-parts manufacturing company, and business is going badly. Sound familiar?

Parts Unlimited has bet the shop on The Phoenix Project, a giant new software release designed to turn the company's fortunes around. They promised investors that it would be delivered in a few weeks. Still, the team is hopelessly behind schedule, and the marketing department keeps adding to the workload through various unofficial back channels. At the same time, frequent firefighting is pulling resources away from Phoenix and causing more delays. It's a vicious cycle from which escape appears to be impossible.

If Phoenix is not delivered on time, Bill knows that he and most of his colleagues will lose their jobs.

The Goal's Jonah is replaced by Eric, a quirky new investor with crazy ideas that challenge Bill's conventional wisdom. Under Eric's mentorship, Bill learns the flaws in his old arguments about managing IT projects. He embarks on a journey to understand "The Three Ways": Flow, Feedback, and Continual Experimentation and Learning.

Along the way, each archetypal character either learns to embrace a new way of working or gets their comeuppance. When I realized that things weren't likely to end well for the feeling I recognized as myself, I knew I had to change.

The most valuable thing about this book is how well it articulated the harm I was doing when I thought I was doing my job well. The Phoenix Project helped me understand my role and the consequences of my actions in a broader and more valuable context. If it weren't for this book, I probably wouldn't be where I am today.

If you enjoyed The Phoenix Project, you'll probably also enjoy [The Unicorn Project](#unicorn), which tells the same story from a very different perspective, and you might be interested in going back and reading [The Goal](#goal). If you'd like to learn more about building great teams, check out [The Five Dysfunctions of a Team](#dysfunc). If you want a more formal overview of the topics raised in Phoenix, try [The DevOps Handbook](#handbook) or [Accelerate](#accelerate).

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/17255186-the-phoenix-project)

### 7. The Unicorn Project (Kim: 2019)  {#unicorn}

The Unicorn Project is a retelling of [The Phoenix Project](#phoenix). It's neither a prequel nor a sequel. It's the same story, on the same timeline, but told from a different perspective.

The Phoenix Project is told from Bill Palmer's perspective, as a senior manager with a background in the operations side of the business. Phoenix talks a lot about lean principles, collaboration, and all that's valuable. Still, Bill has been promoted far enough that he rarely plays with the code anymore and lacks development experience. This can make The Phoenix Project an unsatisfying read for developers, sometimes giving them the impression that you can't do much about the underlying problems unless you are in senior management.

In contrast, The Unicorn Project tells the story of Maxine Chambers. She's a senior developer who's just been relegated to the phoenix project after getting blamed for a disaster that wasn't her fault. Well respected by her team, she's a strong leader who shuns formal management positions because she loves to code.

Alongside some organizational themes, such as corporate bureaucracy, blame culture, and lengthy approval processes, "Unicorn" covers more technical topics, including continuous integration, data management, and functional programming.

The primary focus of Unicorn is "The Five Ideals":

1. Locality and simplicity
1. Focus, flow, and joy
1. Improvement of daily work
1. Psychological safety
1. Customer focus

While Unicorn is undoubtedly aimed at engineers over managers, and developers over operations, it's the pairing of Phoenix and Unicorn that I find so valuable. Frankly, if you like one, you'll probably enjoy the other, and it's enlightening to read the same story from two different perspectives. It's a beautiful exercise for learning to understand and empathize with how the other side sees things.

If you enjoyed the Unicorn Project, try reading [The Phoenix Project](#phoenix) next. If you'd like to learn more about building great teams, check out [The Five Dysfunctions of a Team](#dysfunc). If you'd like to learn more about designing your code for DevOps, try [Domain-Driven Design: Distilled](#ddd), or if you are a data specialist, [Database Reliability Engineering](#dre). Finally, if you'd like to learn more about continuous integration and deployment pipelines, check out either [Continuous Delivery](#cd) or [The DevOps Handbook](#handbook).

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/44333183-the-unicorn-project)

### 8. The DevOps Handbook (Kim, Humble, Debois, Willis: 2016) {#handbook}

This book is perhaps the best articulation of what DevOps is. It's intended as a companion to <a href= "https://www.octopus.com/blog/devops-reading-list#phoenix">The Phoenix Project</a>, and it aims to codify the thoughts and patterns of Phoenix into a more formal and actionable pocket handbook. (Although you need pretty big pockets.)

It opens with an account by John Willis called "The Convergence of DevOps." This is a short and excellent read, describing how various interrelated movements (Lean, Agile Manifesto, Agile Infrastructure, Continuous Delivery, Toyota Kata) all seemed to reach similar conclusions at roughly the same time and how they converged under the banner of DevOps.

The handbook then uses Kim's "three ways" from the Phoenix Project as a logical structure through which it articulates many of the key ideas and practices at the heart of DevOps, including value stream mapping, deployment practices, testing, telemetry, experimentation/learning. There's also a section dedicated to security and compliance.

It's well written too. It's easy to understand with many references to other great books, articles, and videos. It also includes plenty of real-world case studies to demonstrate the theories in practice.

One of the key differentiators of The DevOps Handbook relative to [Continuous Delivery](#cd) (CD) or [Site Reliability Engineering](#sre) (SRE) is its accessibility. It explains the ideas and concepts in straightforward and logical terms. It ties them directly to business values that are relatively easy to understand even by folks who aren't experienced engineers or business leaders. This is why it's an excellent read for IT managers or senior leaders who lack recent technical experience.

This accessibility may also be its downside. I wanted to go deeper on the topics I was already familiar with, but I was left with questions. 

> "How should you handle this unusual scenario?"

> "How would that work in practice?"

If compared with CD or SRE, for example, The DevOps Handbook is less detailed but broader in scope, and it's an easier read as a result. Unlike CD or SRE (which are dense), you may find yourself reading the handbook cover.

The DevOps Handbook is a fantastic read for someone new to DevOps or who wants to understand how the various strands of DevOps fit together. After you finish it, you'll hopefully be inspired to continue your DevOps education by going deeper into the topics that most interest you.

If you haven't read [The Phoenix Project](#phoenix) yet, it's a great companion to The DevOps Handbook as it tells the story of an IT manager who puts "the three ways" into practice. If you want to go deeper on specific topics, you'll likely find plenty of references in the "Handbook" to further reading materials. Most of the books in this post that pre-date the handbook are referenced at some point.

Suppose you're in senior management and interested in more reading material to help you structure your IT organization for success. In that case, I recommend you look at [Accelerate](#accelerate), which takes a scientific, data-driven approach to analyze the data from the State of DevOps reports to make an empirical case for why many of the practices in the handbook deliver business value. You might also enjoy [Team Topologies](#tt), which explores the various team structures that enable or inhibit flow.

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/26083308-the-devops-handbook)

### 9. Accelerate (Forsgren, Humble, Kim: 2018) {#accelerate}

If <a href="https://www.octopus.com/blog/devops-reading-list#handbook">The DevOps Handbook</a> explains “how” to embrace DevOps, Accelerate explains “why”. This is the slam dunk argument for anyone who is either skeptical of DevOps or interested in understanding the relationship between various DevOps practices and business success. It's a great tool for selling DevOps to senior management.

In many ways, the book is a response to the critique that "DevOps" is a buzzword or a cult, full of warm and fluffy ideas that might sound nice and make sense for a small business or start-up but which do not practically scale for large organizations or are not compatible with tightly regulated industries like healthcare or finance.

The authors achieve this by analyzing the data from 2014-to 2017 [State of DevOps Reports](https://www.devops-research.com/research.html). Forsgren, [a well-respected and published researcher](https://nicolefv.com/research), applies various scientific and statistical methods to the data to see what they can teach us. Her findings are striking.

Long story short: The business benefits of DevOps are accurate and predictable.

Despite the profoundly scientific and statistics-driven methods, Accelerate is a relatively short and easy-to-digest book, written in plain English, in a format that should make sense to the technical or the commercial folks in any business.

The book is divided into three parts, each very different.

Part 1 gets to the point, detailing the extraordinary findings in just 130 short, diagram-rich pages. Frankly, if you are new to DevOps, these 130 pages would make an excellent DevOps primer, even if you then decide to switch to one of the other books on this list. 

I'm a fan of audiobooks, and over time I've gradually increased the speed at which I play them. I now listen to them at roughly double speed; anything slower just feels tedious. In the pre-covid era, I used to travel a lot for work. I listened to the whole of Accelerate part 1 in under 90 minutes while driving home from a "DevOps Health Check" style consulting engagement. The book described many of the problems that this and many of my other clients were struggling with.

I was so captivated by what I heard that as soon as I got home, I ordered a hard copy for next-day delivery so I could re-read it more carefully.

Accelerate helped me understand and appreciate many of the issues I regularly witnessed with my customers. Previously, I would have gut instincts that certain practices were harmful, but I struggled to articulate why authoritatively. Accelerate gave me the language and evidence to explain my gut reactions to technical and commercial stakeholders.

While I found part 1 enormously helpful, I've never attempted to read part 2. I don't think it's designed for me. It's an academic discussion about the scientific and statistical methods used to deliver the conclusions detailed in part 1. I'm sure this will be valuable reading to any stats or data geeks who are interested in the methods or for any skeptics who want to find flaws in the logic. 

I enjoy driving and coding, but I couldn't design a carburetor or CPU. Similarly, I recognize that I'm more interested in applying the lessons Accelerate teaches than understanding the scientific and statistical models used to develop them. What matters to me is that the authors' methods work. Given the popularity of the book and the fact that I've not heard any serious criticisms of the authors' methods, my conclusion is that the techniques were probably reliable. (And if they weren't, I'd unlikely be the one to challenge them anyway. I recognize that Nicole Forsgren is better at research and analysis than I am.)

Despite not reading part 2, I did find part 3 helpful. It's a case study from ING Netherlands. It tells the story of a specific organization that applied the lessons from part 1. The authors clearly state that what matters is ING's approach to interpreting the lessons rather than the particular practices they implemented. It's helpful to finish the book since it demonstrates how to implement the theory.

So what are the lessons?

Accelerate places a high priority on the simultaneous and continuous improvement against four key metrics:

1. Lead time
1. Deployment Frequency
1. Mean Time to Restore (MTTR)
1. Deployment Failure Percentage

These four metrics reinforce each other, creating a virtuous cycle, and are predictive of business success as measured by profitability, market share, and productivity.

To achieve business success, Accelerate highlights 24 practical capabilities (such as automating deployments and supporting learning) demonstrated to drive improvement against the four metrics.

Accelerate provides sound evidence and reasoning, which explains why DevOps works as a method for delivering enormous business value. This makes it a great first DevOps book or a gift for a senior leadership team lacking technical experience. For example, if you have read [The Phoenix Project](#phoenix), imagine how much grief Bill Palmer (VP of IT Operations) would have saved himself if he'd managed to persuade Steve Masters (CEO) to read Accelerate in chapter 1.

Suppose your role is a technical one, or you are a senior manager responsible for technical outcomes after reading Accelerate. In that case, you probably want to move on to one of the more practical "how to do DevOps" books, like [The DevOps Handbook](#handbook), [Continuous Delivery](#cd), [Site Reliability Engineering](#sre), [Domain-Driven Design: Distilled](#ddd) or (if you need to tackle people, team, or culture issues before addressing the technical issues) [The Five Dysfunctions of a Team](#dysfunc) or [Team Topologies](#tt). 

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/35747076-accelerate)

### 10. Team Topologies (Skelton, Pais: 2019) {#tt}

Team Topologies uses <a href="https://en.wikipedia.org/wiki/Conway%27s_law">Conway’s Law</a> to bridge the divide between books about designing effective software architectures (e.g. <a href="https://www.octopus.com/blog/devops-reading-list#ddd">Domain-Driven Design: Distilled</a>) and books about creating effective teams (e.g. <a href="https://www.octopus.com/blog/devops-reading-list#dysfunc">The Five Dysfunctions of a Team</a>), while optimizing for the rapid “flow” of value to end users.

The Continuous Delivery movement profoundly influences Matthew Skelton in the UK, and this influence shines through. I know this personally because, for about a year back in 2017, I co-organized the [London Continuous Delivery Meetup Group](https://www.meetup.com/London-Continuous-Delivery/) with him. Attendees would sometimes come with their copy of [Continuous Delivery](#cd) tucked under their arm - and they called it "the Bible". The spin-off [Pipeline Conferences](https://pipelineconf.info/), which Skelton ran, were some of the most welcoming, diverse, and intellectually stimulating tech conferences I've ever attended/supported.

Team Topologies is a book for the senior managers of IT departments. It takes the view that software architecture starts with team architecture and provides a blueprint for designing your teams and the communication/collaboration protocols between them so that your preferred software architecture emerges organically. This radically reduces the need for toxic bureaucracy and the risk of poor architectural choices that accrue significant [technical debt](https://en.wikipedia.org/wiki/Technical_debt).

If you enjoyed Team Topologies and would like to learn more about some of the core concepts it discusses, the three books referenced in the first two paragraphs above are a great start. You might also enjoy [Accelerate](#accelerate), another ideal book for senior IT leadership that uses a scientific, data-driven approach to map various technical and cultural practices to business success. 

For more reviews, as well as procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/44135420-team-topologies)

### 11. Database Reliability Engineering (Campbell, Majors : 2018) {#dre}

> "The book delivers: it's a 250-page version of the concepts in Google's [Site Reliability Engineering](https://octopus.com/blog/devops-reading-list#sre) book (which I love) targeted at people who might currently call themselves database administrators but want to go to work in fast-paced, high-scale companies."

Those are not my words; Brent Ozar wrote them in [his review of "DRE"](https://www.brentozar.com/archive/2017/11/book-review-database-reliability-engineering-campbell-majors/).

As I was compiling this post, I came across Brent's review, and I love it. He said exactly what I wanted to say, but better. He explains how the reader should approach the book, depending on whether they're a DBA, a manager, or a developer/SysAdmin.

My favorite take-aways from DRE were the focus on "resilience over robustness" and the ubiquitous use of SLOs as a method for aligning objectives and improving collaboration across the "wall of confusion" between dev and ops. I also appreciated the focus on "operational visibility" instead of traditional monitoring, which gets to the heart of the current #observability debate.

Brent signs off with:

> "It's the kind of book that's easy to read and hard to implement. Implementing the SLOs described in chapter 2 takes most traditional companies months to agree on and monitor.

> "Over time, the brand names and open source tools will change, but the concepts will be rock solid for at least a decade. This book is a great waypoint marker set about 5-10 years in the future for most of us, but it'll be one you'll be excited to work towards."

[Check out Brent's full review here](https://www.brentozar.com/archive/2017/11/book-review-database-reliability-engineering-campbell-majors/) (but please come back when you are finished).

That pretty much sums it up for "DRE". Thanks, Brent, for saving me a little time!

If you enjoyed "DRE", it's likely you'll also want its big sister, [Site Reliability Engineering](#sre), which is more prominent in size and broader in scope. However, suppose you fancy something a little lighter. In that case, you might enjoy [The Phoenix Project](#phoenix), where an operations team learns to work more effectively with developers and the rest of the business to avoid repeated data-centric disasters. You might also like Phoenix's sister novel, [The Unicorn Project](#unicorn), which tells the same story from the perspective of a senior developer who inherits a monolithic database and is effectively tasked with creating and maintaining a data lake.

If you're struggling to break out a monolithic database into a set of smaller, more loosely coupled databases, you may also benefit from reading [Domain-Driven Design: Distilled](#ddd). Finally, if you're an old-school DBA and remain skeptical about DevOps, I encourage you to look at [Accelerate](#accelerate).

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/36523657-database-reliability-engineering)

### 12. Site Reliability Engineering (Beyer, Jones, Petoff, Murphy: 2016) {#sre}

You've arrived at the heaviest book on this list.

Site Reliability Engineering (SRE) details how Google approaches the continuous delivery and maintenance of its enormous portfolio. It's been so popular and influential in the DevOps community that there is now a growing sub-community that embraces "SRE" as a specific thing either as well as or within "DevOps".

Reading this book is a reasonable time investment, so for those who are new to SRE, I recommend that before you buy it, you explore the following links:

1. This blog post by Google: [SRE vs. DevOps: Competing standards or close friends?](https://www.googblogs.com/sre-vs-devops-competing-standards-or-close-friends/)
1. Thomas A. Limoncelli's 2012 session at USENIX NYC: [SRE@Google: Thousands of DevOps Since 2004](https://www.youtube.com/watch?v=iIuTnhdTzK0)

That 10-minute read / 45-minute watch should give you an excellent primer on Google's approach, covering essential topics, including the difference between DevOps and SRE, as well as some of the core components of SRE, including SLOs, error budgets, and Customer Reliability Engineering.

Then you've got 560 pages covering 34 chapters, detailing some of the technical and cultural practices that Google employs to manage the reliability of its services at scale. There's so much in it that I'm not going to attempt to go further than that about any specific techniques.

While SRE is a fascinating read, it's worth remembering that most of us do not work for organizations near as close to "Google-scale". With that in mind, SRE is most relevant to those working at substantial organizations. 

One of the criticisms of SRE is the way it effectively normalizes and advocates for the existence of a separate SRE (Ops/DevOps) team. My personal view is that most of the DevOps community believes that in most cases, and indeed in most small/medium-sized companies, a team should own the end-to-end lifecycle of their product or service rather than hand "Ops" concerns over to a separate silo.

This concern aside, many of the practices in the book are likely to be broadly applicable and relevant. It may give you ideas about how to solve some of your challenges.

SRE is an excellent read for anyone who self-identifies as being toward the "Ops" end of the DevOps spectrum and for anyone looking for ways to improve the relationships between distinct Dev and Ops teams. For folks who want to go deeper on data and databases, check out [Database Reliability Engineering](#dre) as well/instead. For folks who are more interested in Continuous Delivery challenges rather than operability challenges, consider [Continuous Delivery](#cd). For those who would like to learn more about splitting monolithic systems into a more loosely coupled collection of services, look at [Domain-Driven Design: Distilled](#ddd). For those who liked SRE but don't understand how it differs from DevOps, buy yourself a copy of [The DevOps Handbook](#handbook) for comparison (and, specifically, take a close look at chapter 7). For folks who are torn about whether to set up a special SRE team, you may find some guidance in [Team Topologies](#tt).

For more reviews, as well as a preview and procurement options: [Check out this book on GoodReads](https://www.goodreads.com/book/show/27968891-site-reliability-engineering)

### The Annual State of DevOps Reports

Since 2012, a team of researchers from Puppet and DORA, with the support of various sponsors, have been polling thousands of IT professionals and analyzing the results. [Initially led by Alanna Brown and later by Nicole Forsgren](https://twitter.com/nicolefv/status/1328049610439360515), this research program has provided the DevOps movement with more data-driven, evidence-based foundations than would be possible by any individual author or speaker sharing their own personal experiences.

Forsgren and Humble used the data from the 2014-2017 reports and Kim to produce [Accelerate](#accelerate) in 2018, which I believe remains the best evidence our industry possesses for the value of DevOps.

[You can review all the DORA State of DevOps Reports (2014-2019 at the time of writing) here](https://www.devops-research.com/research.html).

### Beyond The Phoenix Project

Beyond the Phoenix, Project is technically an audiobook, but it's more like a podcast series. It's a recording of a 7-hour conversation between Gene Kim (Co-author of [The Phoenix Project](#phoenix), as well as other titles in this post) and John Willis (co-author of [The DevOps Handbook](#handbook)). 

Kim and Willis start by exploring the history of DevOps from its earliest origins (which Willis claimed go back as far as Charles Darwin in 1859!), and they dig into the life and teachings of various impactful figures along the way, including William Deming, Taiichi Ohno, and Eliyahu Goldratt. 

They then review some of the most significant theoretical foundations of modern DevOps, including Lean Manufacturing and Safety Culture, before taking a practical look at the various DevOps ideas that played out in The Phoenix Project.

They finish with a recording from a session at a DevOps Enterprise Summit event in 2017, where they brought a bunch of experts together to explore the commonalities between Lean and Safety Culture.

It's fascinating to listen from start to finish and one that many people go back to and repeat over and over.

[You can purchase Beyond the Phoenix Project from Audible here.](https://www.audible.co.uk/pd/Beyond-the-Phoenix-Project-Audiobook/B07B7CH7FQ)

### How complex systems fail

When exploring the historical foundations of DevOps, most folks (including myself) immediately jump to Lean Manufacturing, and that's well justified. However, many folks fail to recognize that DevOps owes much to the "Safety Culture" or "Safety 2.0" movement, which has a totally independent and very different history. Arguably, ideas such as agile infrastructure, chaos engineering, resilience over robustness, observability, and blame-free cultures owe more to Safety Culture than to Lean Manufacturing.

Safety Culture is the study of the cause of disasters in complex and often high-risk environments. In IT, we often fall into the trap of believing our regular IT failures should class our work as high risk. That's usually a mistake, and most folks who argue that it isn't, have never worked in the military, a hospital, or the aviation industry, where individuals often make daily life and death decisions. Our deployment screw-ups typically matter a lot less than the screw-ups of a soldier, surgeon, or pilot. It's often worth reminding ourselves about that. (Imagine how much more difficult a blameless post-mortem would be if someone had died.)

However, there is a lot we can learn from folks who genuinely have to manage serious risks daily. In the 1990s, Richard Cook worked in the health care sector and researched patient safety. In 1998 he published a paper called How Complex Systems Fail. It's a relatively short and easy read that summarizes 18 core ideas about the effective management of risk. The crazy thing is that as an IT person if you didn't know he was writing about safety in hospitals, you would probably have thought you were reading about IT.

By reflecting on Cook's research and imagining the implications to one fictional IT organization that embraces DevOps and another that favors old-fashioned waterfall-style project management and bureaucracy, it's easy to understand why the waterfall organization is far more likely to suffer more frequent and severe disasters.

I won't try to summarize the main points of Safety Culture here because it would take too long, and ultimately, I'd just be paraphrasing the same points Cook makes pretty articulately for himself. I encourage you to read the paper; it's only a 10-minute read: [https://how.complexsystems.fail/](https://how.complexsystems.fail/)

## Workshop Feedback

Please consider taking a moment to provide feedback for the workshop you've attended. This will help us improve it for the next attendees. 

[Feedback Form](https://oc.to/workshopfeedback)
