# Docs to READ

## 2022-01

- [x] [Accelerate State of DevOps Report: The Move to Multi-Cloud](pdf/2021-09-21-devops.pdf)
  - [devops](https://devops.com/accelerate-state-of-devops-report-the-move-to-multi-cloud/)

  > [2021 Accelerate State of DevOps Report](https://cloud.google.com/devops/state-of-devops/)
  > - 973x :more frequent code deployments
  > - 6570x:faster lead time from commit to deploy
  > - 3x   :lower change failure rate (changes are 1/3 less likely to fail)
  > - 6570x:faster time to recover from incidents

- [ ] [VMware eases app modernization with official launch of Tanzu Application Platform](pdf/2022-01-11-silicon.pdf)
  - [silicon](https://siliconangle.com/2022/01/11/vmware-eases-app-modernization-official-launch-tanzu-application-platform/)

- [x] [VMware Tanzu Targets Skills Gap, Shifts Security Left](pdf/2022-01-11-sdx.pdf)
  - [sdx](https://www.sdxcentral.com/articles/news/vmware-tanzu-targets-skills-gap-shifts-security-left/2022/01/)

> Kubernetes is not a developer platform

> As we talked to many enterprise customers, there has been a clear [developer experience] gap

> Tanzu Application Platform aims to minimize the challenge of navigating Kubernetes to boost developer productivity.

- [x] [Why Software Is Eating The World](pdf/2011-08-20-wsj.pdf)
  - [WSJ](https://www.wsj.com/articles/SB10001424053111903480904576512250915629460)

- [ ] [Software is Eating the World, Revisited](pdf.2021-08-09-blog.pdf)
  - [Blog](https://eriktorenberg.substack.com/p/software-is-eating-the-world-revisited)

- [ ] [Reflecting on Marc Andreessen’s ‘Software is Eating the World’](pdf/2021-08-20-blog.pdf)
  - [Blog](https://blogs.cisco.com/developer/softwareeatingworld01)

- [x] [Software is still eating the world](pdf/2016-06-08-tc.pdf)
  - [tc](https://techcrunch.com/2016/06/07/software-is-eating-the-world-5-years-later/)

<details>
<summary>TL;DR</summary>

> Today, the idea that “every company needs to become a software company” is considered almost a cliché.

> “Six decades into the computer revolution, four decades since the invention of the microprocessor, and two decades into the rise of the modern Internet, all of the technology required to transform industries through software finally works and can be widely delivered at global scale.”

> For a traditional industrial or service company, making the transition to acting like a software company is a massive undertaking. You need to hire new people in every part of your organization; restructure around different economics; overhaul infrastructure.

> Focus on your core
> As Steve Jobs once famously said, “Deciding what not to do is just as important as deciding what to do.”
> Uber doesn’t own their cars. They also don’t directly employ their own drivers.
> The core application and ecosystem around the Uber experience is their primary asset and differentiator.

> Focusing on your core when it comes to technology makes it easier to focus on your end-customer experience — and that’s what makes a great software company.

</details>

- [x] [What don't people understand about DevOps (yet)?](https://www.protocol.com/braintrust/what-people-misunderstand-about-devops)

<details>
<summary>TL;DR</summary>

> Companies that understand DevOps tend not to use the term “DevOps” at all, nor do they have any "DevOps engineers”.

> DevOps isn't a role. It's a culture.

> Companies that genuinely understand DevOps understand it's not a siloed team or function, but instead a new way of doing business that brings with it a new culture, new processes, embedded SREs, a hyper-focus on automation across the board, a service-based architecture, specific SLOs and an associated budget.

> DevOps shouldn't be one person's concern. It should be an integrated part of your engineering culture to have the most significant impact.

> DevOps isn't just about the speed and agility of software development and delivery. It's also about good security practices.
As DevOps practices improve, DevSecOps naturally follows.

> It is possible to achieve speed without sacrificing security. It starts by rethinking how security fits into your delivery workflow.

> The more security is woven into the best practices of everyone’s job, the easier it is to maintain your desired deployment velocity as well as ensure solid security practices. DevOps helps achieve the balance.

> I often hear people say they want a product for DevOps. But is it possible to achieve consistent DevOps with just a product?
Software development in organizations consists of a variety of requirements. Therefore, a DevOps approach that is adapted to each company is necessary.

> It is a mistake to think that you can just buy a certain technology and immediately achieve DevOps. DevOps is first and foremost a culture and a way of working. Organizations need to move from a tool-first mindset to a team-first mindset.

</details>

- [ ] [Securing the Kubernetes software supply chain](pdf/2021-12-15-infoworld.pdf)
  - [InforWorld](https://www.infoworld.com/article/3644808/securing-the-kubernetes-software-supply-chain.html)

- [x] [What is cloud-native? The modern way to develop software](pdf/2021-08-17-infoworld.pdf)
  - [InforWorld](https://www.infoworld.com/article/3281046/what-is-cloud-native-the-modern-way-to-develop-software.html)

  <details>
  <summary>TL;DR</summary>

  > Cloud-native is a modern approach to building and running software applications that exploits the flexibility, scalability, and resilience of cloud computing.

  > The Cloud Native Computing Foundation (CNCF) defines cloud-native a little more narrowly, focusing on application containerization

  > 1. The application definition and development layer
  > - The top layer of the cloud-native stack focuses on the tools used by developers to build applications

  > 2. The provisioning layer
  > - The provisioning layer of the cloud-native stack includes anything required to build and secure the environment where an application will run, ideally in a repeatable fashion

  > 3. The runtime layer
  > -  The runtime layer concerns anything associated with the running of a cloud-native application

  > 4. The orchestration and management layer
  > - The orchestration and management layer brings together the tools required to deploy, manage, and scale containerized applications, including orchestration and scheduling

  > (v.) Observability

  > Key differences between Clound Native apps and traditional apps
  > - Updatability
  > - Elasticity
  > - Mulititenancy
  > - Downtime
  > - Automation
  > - Stateless

  </details>

## 2021-12

- [x] [App Modernization: Why ‘Lift and Shift’ Isn’t Good Enough](pdf/2021-12-08-thenewstack.pdf)
  - [The New Stack](https://thenewstack.io/app-modernization-why-lift-and-shift-isnt-good-enough/)
  > For instance, less than half of participants in a 2020 survey by Harvard Business Review said their cloud strategy has been effective in terms of IT management, customer experience, and innovation. That failure rate is because many IT organizations just lift and shift — simply re-host to the cloud — to meet artificial deadlines.
  
  <details>
  <summary> 7Rs </summary>

  > 1. Retain
  >  - There will be data that can’t be moved, or mainframe modernization that can be postponed.

  > 2. Re-host.
  > - Move the workload from a virtual machine (VM) to a public cloud. In these cases, lift-and-shift is actually the right fit, especially if on-premise has become too costly.

  > 3. Refactor.
  > - Change the application’s code without changing its behavior, so there’s no change in user experience, but speed or efficiency should improve.

  > 4. Re-architect.
  > - Modify the source code, which often means radically changing architecture to microservices. This usually allows it to use the cloud and improve scalability.

  > 5. Rebuild.
  > - Totally rebuild in a cloud native way.

  > 6. Replace.
  > - Move to an off-the-shelf software-as-a-service product (SaaS).

  > 7. Retire.
  > - Deprecate the application.
  </details>

  > app modernization is a journey, not a destination.


- [x] [When to Choose Cloud Foundry over Kubernetes](pdf/2021-12-02-thenewstack.pdf)
  - [The New Stack](https://thenewstack.io/when-to-choose-cloud-foundry-over-kubernetes/)
  > While a single Kubernetes cluster might be easier to operate than a single Cloud Foundry, managing 100 Kubernetes clusters is several orders of magnitude harder than managing a single Cloud Foundry. 

  > Managing a large number of Kubernetes clusters creates complexity that is not necessary with Cloud Foundry.

  >Kubernetes can be customized much more than Cloud Foundry and therefore accept workloads that Cloud Foundry couldn’t.

- [x] [Complexity is killing software developers](pdf/2021-11-01-infoworld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3639050/complexity-is-killing-software-developers.html)
  > Cloud Native Application marks a clear jump in the level of complexity of our software.

  > Amazon CTO Werner Vogels said during the AWS Summit in 2019. “Was it easier in the days when everything was in a monolith? Yes, for some parts definitely.”

  > Essential is the complexity in the business domain you are working in, the fact that enterprises are extremely complicated environments, so the problems they are trying to solve are inherently complex. The other area is accidental; this is the complexity that comes with our tooling and what we layer on top when solving a problem.

  > The cloud-native era has ushered in the potential for more accidental complexity than ever before

  > The complexity inherent to a huge catalog of available services can become, in certain settings, less a strength than a liability.

  > The key to a good internal developer platform then is finding that balance between self-service for developers who want to get on with the job at hand and abstracting the tasks that are the least valuable, without making developers feel restricted

  > The idea behind having golden paths is not to limit or stifle engineers, or set standards for the sake of it. With golden paths in place, teams don’t have to reinvent the wheel, have fewer decisions to make, and can use their productivity and creativity for higher objectives. They can get back to moving fast

  > Complexity is less the issue than inconsistency in an environment by Craig McLuckie

## Author

[shinyay](https://github.com/shinyay)

- twitter: <https://twitter.com/yanashin18618>
