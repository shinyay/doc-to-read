# Docs to READ

## 2022-01

- [x] [What don't people understand about DevOps (yet)?](https://www.protocol.com/braintrust/what-people-misunderstand-about-devops)
> Companies that understand DevOps tend not to use the term “DevOps” at all, nor do they have any "DevOps engineers”.

> DevOps isn't a role. It's a culture.

> DevOps shouldn't be one person's concern. It should be an integrated part of your engineering culture to have the most significant impact.

> DevOps isn't just about the speed and agility of software development and delivery. It's also about good security practices.
As DevOps practices improve, DevSecOps naturally follows.

> I often hear people say they want a product for DevOps. But is it possible to achieve consistent DevOps with just a product?
Software development in organizations consists of a variety of requirements. Therefore, a DevOps approach that is adapted to each company is necessary.

> It is a mistake to think that you can just buy a certain technology and immediately achieve DevOps. DevOps is first and foremost a culture and a way of working. Organizations need to move from a tool-first mindset to a team-first mindset.

- [] [Securing the Kubernetes software supply chain](pdf/2021-12-15-infoworld.pdf)
  - [InforWorld](https://www.infoworld.com/article/3644808/securing-the-kubernetes-software-supply-chain.html)

- [] [What is cloud-native? The modern way to develop software](pdf/2021-08-17-infoworld.pdf)
  - [InforWorld](https://www.infoworld.com/article/3281046/what-is-cloud-native-the-modern-way-to-develop-software.html)
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

  > Key differences between Clound Native apps and traditional apps
  > - Updatability
  > - Elasticity
  > - Mulititenancy
  > - Downtime
  > - Automation
  > - Stateless

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
