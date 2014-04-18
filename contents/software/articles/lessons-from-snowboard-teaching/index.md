---
title: Lessons from Snowboard Teaching
date: 2014-04-18 12:00
template: article.jade
---

Alongside my programming career, I've spent a few years training and working as a snowboard instructor. I've been consistently surprised by how much crossover there is between the two occupations, and how each one has improved my skills in the other. I wanted to share some thoughts on the similarities between snowboard teaching (or really, formal instruction of any kind) and the work we do every day as software developers.

<figure>
  ![Article photo](pic.jpeg)
  <figcaption>
    Photo courtesy of James Streater
  </figcaption>
</figure>

Teaching snowboarding is a process of communicating very technical concepts to people (ranging from total beginners to very advanced) in a digestible fashion, then analysing their performance, and providing just the right feedback to help them progress to a higher level of performance.

If 'communicating technical concepts' and 'providing feedback' sound like things you often do as a software developer, then great! I think so too!

## The teacher and learner roles

Whether we realise it or not, as software developers we frequently drop into the role of either teacher or learner. Teaching is not necessarily *telling people what to do*, often it's more like *trying to sell someone on a concept - a way of doing something, or a reason why something is happening*. Framed that way, it's easy to spot situations as a developer where you're in a teaching role - trying to sell someone on an idea you have, or a learning role - listening to someone's 'pitch', voluntarily or otherwise, and either accepting it into your 'way of doing things' or not.

### Motivation

The motivations in each of these roles tend to be similar as well.

As a teacher of snowboarding, what I want (beyond the obvious - keeping you safe, enjoying a days work, getting a good tip etc) is to make you a better and more efficient rider, and raise the level of our discussion, in the hope that the riding we do together in future is more interesting, enjoyable, and we have to put in less effort for it. As a 'teacher' of programming - maybe I'm trying to convince you that we should use an existing library rather than building our own solution - I'm hoping that the work we do together in future is more productive, enjoyable, and we have to put in less effort for it.

As a student of snowboarding, I'm motivated by the opportunity to ride at a higher level, and experience different types of riding, because I'm not content to always ride the same way on the same sort of terrain. It's boring to ride well within my comfort level for too long. Experiencing many different types of riding makes me a better rider in general, and equips me with a wider range of techniques for dealing with any situation. Personally, this also perfectly explains what motivates me as a programmer.

### What does it mean?

If we recognise, in our day-to-day interactions, the moments when we adopt the role of teacher or student, then we can take steps to make those interactions easier. Either situation can be initiated by you or someone else - you can choose to present an idea to a co-worker, or you might get asked directly how to do something, either of which makes you the teacher. You might ask someone for advice, or someone may approach you with a proposal, making you the student.

As a teacher, you should be aware that the burden of understanding is primarily on you. If you've ever worked as a teacher/trainer/instructor or otherwise been paid to teach a skill to someone, you will have come to realise that it's **your** job to find a way of communicating the skill that works for the learner. Some people are unwilling learners, and this will occur more frequently in the world of software since it's more likely that the 'teacher' initiates the interaction. In this case, as a teacher, it's  important to 'sell' your point well, as you try to make the learner receptive to the possibility of a better way of doing things. This occurs surprisingly often in snowboard teaching - despite wishing to improve their riding, snowboarders with a lot of experience are reluctant to let go of old habits even if they aren't optimal.

As a learner, if you recognise that you are being taught something, then try to help the teacher out. This can be difficult if the 'lesson' is that you've done something that the teacher believes to be incorrect, and you believe otherwise. Nevertheless, your rebuttal will be better informed if you first understand exactly what is being communicated to you. How would you behave if you were paying your co-worker to teach you this lesson (however unlikely that is)? You'd likely ask for clarification on unclear points, explain *why* you have difficulty understanding something, try the thing out immediately to get feedback on it, and repeat your understanding of it back to the teacher in your own terms. It's easy to get defensive when someone makes you an unwilling learner, but it's in everyone's best interest to help people out in their quest to teach you something.

## Feedback

An important part of the teaching process is the way in which we deliver feedback. This doesn't mean 'annual progress review' style feedback, but rather how we evaluate performances on a day-to-day basis, and in software this particularly applies to code review.

### Types of feedback

Feedback can be *intrinsic* or *extrinsic*, and extrinsic feedback can be *informative*, *evaluative* or *corrective*. **Intrinsic** feedback comes from within the performer. In snowboarding, examples of this would be listening to the sound your snowboard makes to determine if you're carving a clean line through the snow or making a more skidded turn. The software equivalent of this might be 'code smells' - various telltale signs that help you recognise when a piece of code is in danger of becoming problematic.

**Extrinsic** feedback comes from outside the performer, generally provided by a teacher or peer (in snowboarding this also covers watching yourself on video, but that has no analogue in software).

**Informative** feedback tells the performer *what* they did. In snowboarding the rider cannot see themselves ride so this is very useful (e.g. 'your heelside turn had a larger radius than your toeside turn' or 'you got about 3 feet off the ground'). In software we can always see the code we've written but sometimes lose sight of the bigger picture (or the more detailed view), so it can be helpful to receive some purely informative feedback ('this method is 30 lines long and has 5 levels of nesting', 'this will navigate to the next page even if validation fails')

**Evaluative** feedback is extrinsic, and is when we judge something against some criteria (e.g. established coding standards or implicitly agreed-upon ideas about good code), but without suggesting how to proceed. 'That was great' or 'that was terrible' are not particularly helpful examples of evaluative feedback. In snowboarding, you might hear 'your range of movement was *not enough* to prevent the board skipping out'. More useful software examples could be 'I cannot quite tell what the foo variable gets initialised to - that part is unclear' or 'you really made this code more intention-revealing and easy for newcomers to understand'.

**Corrective** feedback is when we suggest how something could be improved, 'if you move your weight more towards the tail of the board, it will grip through the end of the turn instead of washing out'. This is crucial in software development. All too often we tend towards subjective evaluative feedback when we should be leaning towards objective evaluation and corrective feedback, especially for more junior developers, e.g. 'this method would become more intention-revealing if you split the body of the loop out into another method', 'moving this calculation outside the loop would improve the performance of this often-used method' or 'changing the variable name and indentation as follows will bring this code in line with our style guide'.

## Conclusion

When giving feedback to a co-worker, in the form of a code review, performance review, or simply responding to an idea they presented, try and spot which type of feedback you're giving. Ask yourself whether it's the most helpful type of feedback you *could* be giving them. Perhaps your **evaluative** feedback is not strongly rooted in objective criteria and you could refer to documented best practices. Maybe **corrective** feedback would be far more helpful, or maybe you'd actually help more with some **informative** feedback to lead the person towards spotting their own mistake.

Try and recognise the times when you're being taught, and the times when you're teaching. If you accept the earlier premise that teaching is largely about 'convincing' people, then you might be surprised how much teaching (attempted teaching, at least) really takes place at the office. Look for opportunities to be an effective teacher, and a willing learner, to make these interactions smoother.
