---
layout: "page_project"
title: "Hybrid Servoing: Reliable Manipulation under External Contacts"
subtitle:   ""
header-img: "contact.jpg"
comments: false
---

<style>
p.publication {
  margin: 0 0;
  line-height: 1.1;
}

p.publication > ptitle {
  color: #241663;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
}

p.publication > authors {
  font-style: italic;
  font-size: 15px;
}

p.publication > authorsb {
  font-weight: bold;
  font-style: italic;
  font-size: 15px;
}

p.publication > conf {
  font-style: normal;
  font-size: 14px;
}

a.links {
  margin: 0 0;
  text-decoration: none;
  font-size: 14px;
}

</style>

Human manipulation dexterity benefits a lot from utilizing external contacts. However, it is still hard for a robot to safely and reliably use external contacts. A small error or disturbance in the system can cause the robot to crash, or the desired contact mode to break.

## Hybrid Servoing
Given a manipulation motion plan (that involves external contacts on the object), what is the most reliable way to execute it? Traditional industrial robots use position control, which is precise and robust against disturbances. However, since the stiffness is super high, the type of control has little tolerance to modeling errors. The robot can easily crash when following a not-so-precise trajectory. On the other hand, using low-stiffness control such as force control won't crash anything. For example, its safe to command a Baxter or Franka robot to move against a wall. However, the compliance sacrifices disturbance rejection ability, so the position control is not accurate or robust.

We believe the right solution is to combine the advantages of both worlds. Being compliant (using force control) in some directions could avoid over-constraining and maintain desired contacts, while being rigid (velocity/position control) in other directions can keep the disturbance rejection ability for executing the motion plan. And such control scheme already exists: they are called *hybrid force-velocity control (HFVC)*.

The question is, given a motion plan, how do we compute the most reliable HFVC control law to execute it? We call this problem the ***Hybrid Servoing*** problem.

In this work, **we provide a solution to the hybrid servoing problem** in a generic form. At each time step, our algorithm computes the dimensionality, directions and magnitudes of force control and velocity control, so as to avoid crashing, maintain desired contacts and satisfy the goal velocity. We quantify the robustness of a control action and make trade-offs between different requirements by formulating the control synthesis as optimization problems. We demonstrated by experiments the effectiveness of our method in several contact-rich manipulation tasks.

{% youtube KtSNmvwOenM %}

Since we optimize for robustness, the resulted motion is very reliable. Below is an uncut 25min video of 50 block tilting experiments, 47 of them succeed.

{% youtube YIP8xIFATHE %}

The project is published in the following paper.
<p class="publication">
    <ptitle> Robust Execution of Contact-Rich Motion Plans by Hybrid Force-Velocity Control </ptitle>
    <authorsb> Yifan Hou </authorsb> <authors> and Matthew T. Mason </authors>
    <conf> In Proceedings of 2019 IEEE International Conference on Robotics and Automation (ICRA) </conf>
    <a href="https://www.ri.cmu.edu/publications/robust-execution-of-contact-rich-motion-plans-by-hybrid-force-velocity-control/">Paper</a> · <a href="https://github.com/yifan-hou/pub-icra19-hybrid-control"> Code </a>
</p>

## Robustness Criteria
How to evaluate a controller for a task? We note that failures in manipulation are usually marked by or caused by unexpected changes of contacts (object slipping away between ﬁngers; getting stuck somewhere, etc). In this work we propose a set of criteria to quantify the robustness of contacts against modeling uncertainties and disturbance forces. Under the quasi-static assumption, we analyze the causes of contact mode (sticking, sliding, disengaged) transitions and discuss how to endure larger uncertainties and disturbances. We summarize our results into several physically meaningful and easy-to-compute scores, which can be used to evaluate the quality of each individual contacts in a manipulation system. We illustrate the meaning of the scores with a simple example.

<p class="publication">
    <ptitle> Criteria for Maintaining Desired Contacts for Quasi-Static Systems </ptitle>
    <authorsb> Yifan Hou </authorsb> <authors> and Matthew T. Mason </authors>
    <conf> In Proceedings of 2019 International Conference on Intelligent Robots and Systems (IROS) </conf>
    <a href="https://www.ri.cmu.edu/publications/criteria-for-maintaining-desired-contacts-for-quasi-static-systems/">Paper</a>
</p>

## Use Passive Compliance for Hybrid Servoing
The Hybrid Servoing algorithm above outputs a hybrid force-velocity control(HFVC). However, implementing a HFVC controller could be a pain. Good news is that you don't have to do HFVC: in this work we show that you can also do manipulation under external contacts with passive compliance.

More specifically, we use suction cups as the example, but the method should work for soft fingertips in general. Suction cups are the most common manipulation effectors in industry for pick-and-place. We show that they can do a lot more than pick-and-place when external contacts are present.

We propose a general framework for manipulation with suction cups under external contacts. The solution consists of a locally linear force-deformation model for suction cups with large deformation, and an estimation-control framework which utilizes contact constraints and feedback control to counter modeling errors. We verify the efficacy of our method experimentally by tilting a block on a table with a suction cup. Our method works reliably under modeling error even under large suction cup deformation (over 40 degree of bending). We also show the superiority of suction cups by performing tasks that are not possible with any normal fingertip.

{% youtube eK77vK8wkUE %}

<p class="publication">
    <ptitle> Manipulation with Suction Cups using External Contacts </ptitle>
    <authors> Xianyi Cheng, </authors> <authorsb> Yifan Hou </authorsb> <authors> and Matthew T. Mason </authors>
    <conf> 2019 International Symposium on Robotics Research (ISRR) </conf>
    <a href="https://xianyicheng.github.io/files/cheng_isrr19.pdf">Paper</a>
</p>
