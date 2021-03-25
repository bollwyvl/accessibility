# All JupyterLab Accessibility Meeting Minutes

This file collects all the separate note files into one place to make it easier to skim the notes or search for topics. It is organized oldest to newest.

## 09.30.20 Meeting Minutes
### Attendees
Martha (@marthacryan )
Max (@telamonian )
Karla (@karlaspuldaro)
Alek
tony (@tonyfast)
Alex (@ajbozarth)
Isabela (@isabela-pf)

### Notes
#### Say hello! 
Introduce yourself however you like. What do you want to get from 
this meeting?
- Our group has limited experience with accessibility work previously. 
We are all learning. Hooray!
- No one here uses a screen reader or other assistive software.
- Should we do outreach to have people involved who use this? 
Probably. Find a way how.

#### Why this meeting? Why now?
- Multiple JupyterLab team meetings where we discuss people's 
interest in making JupyterLab accessible, but those interested 
don't know where to start (both in learning about accessibility 
and wrangling JupyterLab).
- Let's be resources for each other! Share skills, knowledge, 
and morale.
- 3.0 release plans to have a lot of added features, 4.0 might 
be a good time to push for improving what is already there.
  - yes definitely, no way is this getting in 3.0

#### What goals do we have?
- WCAG specifications. Let's review them and figure out how to 
implement them.
    - https://en.wikipedia.org/wiki/Web_Content_Accessibility_Guidelines
    - We reviewed this document to start getting on the same page.
- Get different people involved. Get people who actually use 
accessibility features/ screen readers/ assistive software. 
    - Avoid single point of failure problems. Community engagement 
    needs to be done together.
- Are consoles a good place to start? Some older consoles are 
established and already have accessible affordances for us to 
start working with.
- - Another resource exploring what a typically inacessible 
experience (web comics) can be like with affordances.https://comica11y.humaan.com/ 
(comics use cells too… :eyes:)
- https://design.chicago.gov/accessibility/tools/
- Need a plan to reviewing/getting feedback on JupyterLab as is and 
the changes we make. Can't just rely on accessing disability 
communities because it's our responsibility to fix it.

#### What are people working on?
- Max
  - accesible slider Widget
    - PR: https://github.com/jupyterlab/jupyterlab/pull/9104
    - probably a one-off, not really reusable in current form
  - `LabButton`
    - fully accesible replacement for current blueprint-based 
    `Button` in @jupyterlab/ui-components
    - working on PR, hopefully have an initial stab done by the 
    meeting
    - based on
      - https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/button_role
      - https://www.w3.org/TR/wai-aria-practices-1.1/examples/button/button.html
      - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#Accessibility_concerns
    - tricky part: the button text
      - the reccommendation: always use an HTML button element, 
      always label like <button>text</button>
      - for icon buttons (eg all of our toolbar buttons), the 
      suggestion is to hide the text using CSS
      - [example CSS](https://css-tricks.com/places-its-tempting-to-use-display-none-but-dont/)
        ```css
        .hide {
          position: absolute !important;
          top: -9999px !important;
          left: -9999px !important;
        }
        ```
        
        or
        
        ```css
        .visuallyhidden { 
          position: absolute; 
          overflow: hidden; 
          clip: rect(0 0 0 0); 
          height: 1px; width: 1px; 
          margin: -1px; padding: 0; border: 0; 
        }
        ```
      
      - seems convoluted, can we just use 
      [`aria-label`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute) 
      (this is exactly what it's for)? [Opinions seem mixed](https://developer.paciellogroup.com/blog/2017/04/what-is-an-accessible-name/)
  - I need resources to finish hashing out the styling system for the 
  `LabFoo` components
  - bigger picture: as concrete problems arise (like the text vs 
  aria-label thing for LabButton), we should use them as a jumping 
  off point to seek outside expert opinion/help

- Isabela (and tony, Gonzalo, Eric)
    - Color contrast https://github.com/jupyterlab/jupyterlab/issues/8832

#### Next steps
- Do we want to share these notes somewhere (team-compass)?
- Martha and Max working on UI components (LabButton?)
    - Alek might help too!
- Spend an hour introducing everyone to JupyterLab UI so we 
understand what we are working with and start identifying places 
to work with it. (Do this later when people have done some 
exploration first)
- Removing UI components based on blueprint
- Reach out to Chris Holgraf, Tania Allard, and Jason Grout about 
contacts we've made in this area already (tony)
- Find and share resources (everyone)
- Settings UI (Alex). Will start after JupyterCon. Needs 
accessibility reveiw for the design.
- Meet every other week (twice a month).

## 10.21.20 Meeting Minutes
### Attendees
Max @telamonian
Isabela @isabela-pf
Martha @marthacryan
Alex @ajbozarth
Jason Grout @jasongrout

### Notes

#### Logistic check in 
- Does this time seem like it will keep working? Yes.
- If so I’d rather schedule it further out and add it somewhere 
more public so people can drop in. I can bring this up in JLab 
team meeting too, if so.

#### Proposed Goals
We'd like to propose concrete accessibility goals would be so that 
we can organize it into JupyterLab's release cycle and encourage 
people to focus on them. These are some ideas of where to start.
- Max brought up screen readers. Find most common and start from 
that paradigm.
  - discussion on github: https://github.com/jupyter/accessibility/issues/14
- Keyboard accessibility.
- Closing accessibility issues that already exist. There's already 
been work pointing out some of the issues (like here 
https://github.com/jupyterlab/jupyterlab/issues?q=is%3Aissue+is%3Aopen+web4all)
- Can we produce guidelines/docs/resources (or something similar)? 
This might help other people get involved and make the effort more 
sustainable.
- Creating an actionable plan and possibly getting some grant 
money/full time help

#### What are people working on?
Isabela
- Reached out to Tania Allard and Chris Holdgraf. They made point 
to keep all discussions online, so there shouldn’t be anything we 
are missing. Haven’t heard from Tania. This just means I’m trying 
to collect and understand what has already happened so we don’t 
redo or overlook existing work.
- Here’s some common places these discussions live (in Jupyter):
    - Jupyter Discourse accessibility Category https://discourse.jupyter.org/c/special-topics/accessibility/29
    - Jupyter accessibility repo https://github.com/jupyter/accessibility
    - JupyterLab accessibility issue label https://github.com/jupyterlab/jupyterlab/issues?q=is%3Aopen+is%3Aissue+label%3Atag%3AAccessibility
    - Jupyter Notebook accessibility issue label https://github.com/jupyter/notebook/labels/tag%3AAccessibility
    - JupyterHub accessibility issue label https://github.com/jupyterhub/jupyterhub/labels/accessibility
- Accessibility resource doc. WIP. Please feel free to add so we can 
help each other learn. Don’t let it get in the way of doing other 
work, but add as you find useful things. https://docs.google.com/document/d/12cusZV0j91yZTty_BQndorwTIgRloKR7WEWP2aGNp5A/edit?usp=sharing

#### Next steps
- Install NVDA or JAWS and gain familiarity with screen readers 
in general as well as JupyterLab
- Isabela needs to triage existing JupyterLab issues so we can 
assign/move forward with them
- Try and reconvene hackathon group to make sure we are understanding 
the same issues and have proper context to move forward and not 
repeat work that's already been started.
- Explore Phosphor and Lumino accessibility issues and PRs. This 
might be the metaphorical root of a lot of our problems. 
    - Big PRs in the DOM and menu system that started but did not 
    get finished
- Look for grants for funding a full-time accessibility dev
- Schedule meeting with Jason catching us up on work that's been 
done in Phosphor
- Explore Firefox accessibility tools. They've been recommended 
as a good starting point.

## 11.04.20 Meeting Minutes
### Attendees
Martha @marthacryan
Max @telamonian 
Alex @ajbozarth 
Jason @jasongrout 
Isabela @isabela-pf 

### Notes

If needed, recap/point to the notes and resources for our Phosphor 
PR meeting last Monday for people who weren't able to make it.
- Covered what decisions were made and our current goals (transfer 
the problems we already know about in Phosphor to Lumino and finish 
off what was originally Hack4All work).

Are these meetings something we'd want to have on the Jupyter 
community calendar?
- Yes! It will be brought up in next week's JupyterLab team meeting 
for approval/necessary steps.

- Need to see if we can find or get data on what developers who use 
screen readers use in terms of OS

#### What are people working on?
- Martha: [#129](https://github.com/jupyterlab/lumino/pull/129) - 
Moved PR from phosphor to lumino, reviewers?
- Gonzalo: Following up on Phosphor tutorial videos. Confirmed we 
can repost them, but need to get license.
    - Also need a PR for Lumino docs once the videos get set up.

#### Next Steps
- Alex: Review [#129](https://github.com/jupyterlab/lumino/pull/129) 
Add isToggleable command state.
- Gonzalo: Get final info about reposting Phosphot tutorial videos 
for Lumino docs
- Isabela: Move Phosphor issues to Lumino. Also consolidate issues 
from other repos where relevant so we don't have to look for issues 
across as many repos anymore.
- Goal
    - Once those three Phosphor PRs are fully up and ready to be 
    reviewed/merged, then we can reach out to experts to talk more.
    - Potentially asking for  a meeting where we watch experts 
    test PRs so we can learn how to better test too (and not just 
    rely on them).

## 11.18.20 Meeting Minutes
### Attendees
Martha @marthacryan
Karla @karlaspuldaro
Alex @ajbozarth
Max @telamonian
Jason @jasongrout 
Thomas @manfromjupyter
Isabela @isabela-pf 

### Notes
- Welcome Thomas!

#### What are people working on?

- Martha
    - PRs [jupyterlab/lumino#129](https://github.com/jupyterlab/lumino/pull/129) 
    and [jupyterlab/lumino#131](https://github.com/jupyterlab/lumino/pull/131) merged!
    -Hooray for Martha! Great job getting that done!

- Max
    - Requesting review on [jupyterlab/lumino#132](https://github.com/jupyterlab/lumino/pull/132) 
    rebasing for lumino.

- Isabela
    - PR for JupyterLab color contrast updates at 
    [#9335](https://github.com/jupyterlab/jupyterlab/pull/9335). 
    This means it has a binder to test. Original issue is 
    [#8832](https://github.com/jupyterlab/jupyterlab/issues/8832)
    - Started sorting through the web of repos where accessibility 
    work was started as issues (based on Phosphor Walkthrough 
    meeting notes). Nothing to show yet.

#### Next Steps
- Martha will test her PRs with NVDA.
- Martha will make an issue for isToggleable additions to 
[#9365](https://github.com/jupyterlab/jupyterlab/issues/9365). 
Will also start working on it.
- Max will update [jupyterlab/lumino#132](https://github.com/jupyterlab/lumino/pull/132) 
with the items on the checklist.
    - Also create a binder.
- Thomas will review JupyterLab and perform an audit of all/most of 
the accessibility issues needing to be addressed to ensure an 
optimal user experience for all users with visual, auditory, 
ambulatory, or cognitive handicaps. Goal will be to uncover all 
that is needed to become fully WCAG 2.1 compliant. Will be using 
JAWS for the screenreader when a screenreader is necessary, but 
reported issues will be for all of them, not screenreader specific.
    - Setup following https://jupyterlab.readthedocs.io/en/latest/developer/contributing.html
    - maybe `pip install —pre jupyterlab`
    - Post issues to [jupyterlab repo](https://github.com/jupyterlab/jupyterlab) 
    with [accessibility label](https://github.com/jupyterlab/jupyterlab/issues?q=is%3Aissue+is%3Aopen+label%3Atag%3AAccessibility).
- Isabela will consolidate the accessibility issues across repos 
where appropriate (probably [jupyterlab](https://github.com/jupyterlab/jupyterlab) 
or [lumino](https://github.com/jupyterlab/lumino)). Will bring the 
new issues for the next meeting so we can keep moving forward with 
the problems we already know about.

## 12.02.20 Meeting Minutes
### Attendees
tony @tonyfast
Max @telamonian 
Jason @jasongrout 
Alex @ajbozarth 
Karla @karlaspuldaro
Gonzalo @goanpeca 
Martha @marthacryan 
Thomas @manfromjupyter 
Darian @afshin 
Isabela @isabela-pf 

### Notes

- There are overlap in infrastructure needs for an accessible 
JupyterLab and mobile/tablet support for JupyterLab. Maybe this 
is an opportunity to get more people involved in this work since 
there have been a lot of requests for mobile/tablet support.

Triage of existing accessibility issues
**This will be cross-referenced, updated with #9399, and stored 
in this [project](https://github.com/orgs/jupyterlab/projects/1) 
from here on out.**
- Reviewed from [diagram-codesprint/phosphor](https://github.com/diagram-codesprint/phosphor), 
[diagram-codesprint/jupyterlab](https://github.com/diagram-codesprint/jupyterlab), 
[phosphorjs/phosphor](https://github.com/phosphorjs/phosphor/), 
[jupyterlab/lumino](https://github.com/jupyterlab/lumino/), and 
[jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab/labels/tag%3AAccessibility) 
([jupyter/accessibility](https://github.com/jupyter/accessibility/issues) has been more organizing focused).
- Isabela proposes continuing to focus on what was found in Hack4All first.
    - [#6577](https://github.com/jupyterlab/jupyterlab/issues/6577)
    - [#6578](https://github.com/jupyterlab/jupyterlab/issues/6578)
    - [#6579](https://github.com/jupyterlab/jupyterlab/issues/6579)
    - [#6580](https://github.com/jupyterlab/jupyterlab/issues/6580)
    - [#6581](https://github.com/jupyterlab/jupyterlab/issues/6581)
    - [#6582](https://github.com/jupyterlab/jupyterlab/issues/6582)
    - [#9365](https://github.com/jupyterlab/jupyterlab/issues/9365) Follow up for jupyterlab/lumino #129 that applies isToggleable to JLab now that it is possible with Lumino (Martha started this!)
    
- Issues Isabela wants to look into more
    - JLab [#6575](https://github.com/jupyterlab/jupyterlab/issues/6575) 
    (update of diagram-codesprint/jupyterlab #8) Has merged PR #6359, but 
    didn’t close the issue.
    - JLab [#6576](https://github.com/jupyterlab/jupyterlab/issues/6576) 
    (update of diagram-codesprint/jupyterlab #9) and [#6404](https://github.com/jupyterlab/jupyterlab/issues/6404) Looks like a reference for UX of these accessibility changes and proposed solutions.
    - JLab [#1095](https://github.com/jupyterlab/jupyterlab/issues/1095) 
    Visual/additional/any cues for running commands (this was to be put 
    to phosphor, review if it was already done or not)
    - JLab [#911](https://github.com/jupyterlab/jupyterlab/issues/911) 
    An audit issue about what seems to be the first JLab 
    accessibility review. I need to check if they are or need to be 
    represented in other issues.
    - diagram-codesprint/phosphor [#2](https://github.com/diagram-codesprint/phosphor/pull/2) 
    and [#3](https://github.com/diagram-codesprint/phosphor/pull/3) 
    status. Did they get merged into Phosphor ever?
    - diagram-codesprint/jupyterlab [#4](https://github.com/diagram-codesprint/jupyterlab/pull/4) 
    and [#11](https://github.com/diagram-codesprint/jupyterlab/pull/11) status. 
    Did they ever get merged into JupyterLab?

- Other issues
    - [#6573](https://github.com/jupyterlab/jupyterlab/issues/6573) 
    NVDA tests on JLab. (Not explicitly tied to Hack4All, but seems 
    like it was part of it.)
    - [#4878](https://github.com/jupyterlab/jupyterlab/issues/4878) 
    Older screen reader evaluation with good discussion. Has been 
    mentioned in a few issues and PRs so it would probably be good 
    to brush up on.

#### What are people working on?
- Max and Jason
    - [jupyterlab/lumino#132](https://github.com/jupyterlab/lumino/pull/132) 
    still needs review.
- Thomas
    - Opened [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399)
    - This is a full review of JupyterLab accessibility, can be 
    broken up into other issues as we go.
    - Evaluation is on JLab v.2.26 This should catch a lot of 
    what holds over to 3.0, but we will be facing new problems 
    with virtual notebook.
    - We started discussing how we pull this apart to tackle it
        - Tabs/tab order are the blockers that prevent further 
        evaluation, so they should be high up on our list
        - Order top to bottom should work in order of what are 
        most critical and/or rely on one another
    - This is a great review! Thank you so much!
- Isabela
   - Collecting and triaging existing issues as listed above.

#### Next Steps
- Max created a project to track JupyterLab accessibility work 
https://github.com/orgs/jupyterlab/projects/1. This will be how 
we organize and keep track of work in the future.
- Isabela and Tony will compare and consolidate #9399 with 
pre-existing issues.
    - Isabela also needs to check for duplicate issues and 
    close/update as needed.
    - Triage marking by WCAG standard and maybe level of complexity?
- Martha #9365 applying isToggleable to JLab now that it is 
possible in Lumino is still happening. This will be her next step.
- Time to reach out to experts and say we want to meet in the 
future (also gives us a deadline for some of the commitments)

## 12.16.20 Meeting Minutes
### Attendees
- Tony Fast @tonyfast
- Jason Grout @jasongrout
- Gonzalo Peña-Castellanos @goanpeca
- Martha Cryan @marthacryan
- Sam Kacer @SamKacer
- Thomas @manfromjupyter 
- Alex @ajbozarth 
- Max @telamonian 
- Isabela @isabela-pf

### Notes
- This is the [project for tracking accessibility 
work](https://github.com/orgs/jupyterlab/projects/1). We are still 
figuring out permissions, and this is a work in progress pulling 
over the past triaging work. When 3.0 is out, we want to convert 
the cards into a concrete road map.
- Recommended resource [WAI ARIA authoring practices](https://www.w3.org/TR/wai-aria-practices-1.1/)
- Thomas thinks there are a magic few lines of code that would be 
easy to get in JupyterLab before 3.0 and could make a big difference. 
Posted (and linked above) at [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491)
(formerly team-compass #114).

These discussions have identified four main accessibility needs 
for JupyterLab (can probably be extended to other Jupyter projects 
too)
- Making JupyterLab accessible for a read-only type experience
    - This is the focus of the report on [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399) 
- Making JupyterLab accessible for an interacting/coding experience
- Adding JupyterLab docs for accessibility features
    - Sam gave an anecdote about help pages in docs that lists 
    help and resources for screen reader users.
- Adding CI or relevant accessibility tests to the JupyterLab 
contributing workflow ensure accessibility remains a priority
    - Referenced pydata-sphinx-theme [#292](https://github.com/pandas-dev/pydata-sphinx-theme/issues/292)
     and https://github.com/pandas-dev/pydata-sphinx-theme/runs/1507397117?check_suite_focus=true
    - nteract has some kind of accessibility CI they use 
    (probably focused on react)

#### JupyterLab Code Editor
Our main focus today is the accessibility of JupyterLab's code 
editor as discussed in [#4878](https://github.com/jupyterlab/jupyterlab/issues/4878) 
and the comments of [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399).
- What steps do we want to take?
    - We will be shipping jupyterlab 3 before the end of the year. 
    Changing the default editor would be difficult before 4.0 
    because of the number of things that have started to rely on 
    CodeMirror.
    - Start with an extension based approach. To take action now 
    and eventually fit it in to the release cycle as a part of core.
    - What editor should we start working with?
        - Sam confirms codemirror 6 is working better so far, 
        especially better than we have now.
        - Based on the [JupyterLab Monaco Plugin](https://github.com/jupyterlab/jupyterlab-monaco), 
        is it possible/relatively simple thing to bring that up to 
        date and test how it would work with the editor now.
        - Sam still prefers monaco based on current usage.  

- Where does this fit on our priority list/who can work on this? 
One potential path:
    1. Get monaco editor extension up to date.
    2. Review how that works with screen readers in JLab now. 
    3. Set up a way to quickly and easily install the extension 
    (link for screen readers at top of JupyterLab?) and immediately 
    use it to test screen reader accessibility in JupyterLab.
    4. Prepare the extension to be a part of core JupyterLab for 
    the next release.

- Sam's next priority (after editor) would be the toolbar
    - Needs to conform to what user expect for menu bar interactions
        - Examples: alt focuses menu bar, move between top items 
        with arrow keys.
    - Elements of the menu bar to be marked up with ARIA so it can 
    be communicated via screen reader
        - This is brought up as a part of [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399)

- Jupyter Notebook is just a little more accessible than Lab. "Like 
you get in a car and everything is backwards."

#### Agenda items not yet covered
- is this closed? can someone audit it? https://github.com/jupyterlab/jupyterlab/issues/6575
    - https://github.com/jupyterlab/jupyterlab/pull/6359
- some old audits
    - https://docs.google.com/document/d/1oSHOqmtua_3vdoJddvo4u3na71cIZlpEgP73w-0uXFU/edit#heading=h.umcyl9debp28
    - https://docs.google.com/spreadsheets/d/1RWEtBtXEF5vQf_vJzqtGWnPbT0VZI_RZ_H7RWHmgyGs/edit#gid=0
- Should these minutes be somewhere besides one long issue? Could 
the jupyter/accessibility repo (or another repo) hold minutes in 
a way that allows for more organization?
- Agenda item from Chris Holdgraf (Did Max mention they had already 
been discussing this?)
> 1. Don't forget that we have a little bit of funding from 
Bloomberg to run some kind of event around accessibility. I'm not 
sure how much flexibility we have with it, but perhaps it is worth 
discussing if / how this funding could be useful in a future meeting? 
> 
- how should we handle touch events re accessibility?
  - PR for manually converting some touch events to mouse events
    - https://github.com/jupyterlab/lumino/pull/123

#### Next Steps
- Continue moving past triage work to the [project](https://github.com/orgs/jupyterlab/projects/1) 
for tracking (Isabela)
- Follow up on necessary ARIA roles JupyterLab needs (a [lumino PR](https://github.com/jupyterlab/lumino/pull/131/files) 
already started labeling) (Martha)
- Make issue about menu bar focus (no assignment?)
- Update [Monaco plugin](https://github.com/jupyterlab/jupyterlab-monaco) 
for 3.0 (Max post-3.0)
- 3.0 Release! (Jason and Max)
- Review Max's PR (Martha)
- Reach out to accessibility experts we've met with before (Isabela)
- Check the status of [#6575](https://github.com/jupyterlab/jupyterlab/issues/6575) (Isabela)

## 12.30.20 Meeting Minutes
### Attendees
- Gonzalo @goanpeca 
- Tony @tonyfast
- Thomas @manfromjupyter 
- Isabela @isabela-pf 

### Notes
- From JupyterLab Team meeting 12.23.20 discussion
    - > Is single-document mode the more accessible UI? [compared 
    to JupyterLab default]
    - Thomas says Classic is better, but since that's not being 
    updated we need to keep it relevant
    - Can't move tabs on a screen reader
    - Focus on navbar and notebook. Will this help make jupyterlab 
    and classic accessible together?
    - Having less things on screen could be helpful because it 
    means you can focus on having those things being navigable, 
    but it also can risk hiding functions and making things less 
    usable.
    - jaws, nvda, focus on low vision ambulatory users because at 
    the moment things are completely inaccessible to blind users 
    and will keep being so until we fix these needs first.
    - project manager to get different places. need a foundation.
    - Can't currently evaluate JLab well because you can't even 
    navigate it right now. Keyboard accessibility and tab order 
    are key place to start.

- Agenda item from Chris Holdgraf: "Don't forget that we have a 
little bit of funding from Bloomberg to run some kind of event 
around accessibility."
    - We agreed that we need to follow up on how much money this is 
    to know what we want to do with it.
    - Parts of the work might be good/more contained project that 
    we can get funding for. Maybe the accessible editor is an option?
 - What's the strategy?
    - Thomas would like to see all [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399)
     and [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491) 
     in next six months. These issues make JupyterLab 
     navigable/readable so that it can be more finely evaluated and 
     so that you can even reach the editor experience.
    - Currently can't create new notebooks, or change kernel with 
    keyboard alone?
    - 6 months: everyone but blind users can use jupyter
    - 12 months: everyone can use JupyterLab
    - Can we convince people to act by framing some of these 
    things as helping multiple problems (like a better mobile 
    experience)?
    - Would not recommend splitting the team up because we don't 
    have a lot of people who have an accessibility background, so 
    it might be best to keep our knowledge together.

- Goals for next JupyterLab release? What would we want to 
prioritize?
    - We think we can do it without formally being a part of 
    the release schedule. See above for priorities.
    - Do the work, show it, and it is usually easier to get 
    it incorporated.

### Next steps
- Mark which things are we looking to work on first and make 
sure they are ready to be assigned next meeting (Isabela).
- Look into having regular sprints or other group times to 
work so we can help learn from each other.
- Have a happy new year!

## 01.13.21 Meeting Minutes
### Attendees
Max @telamonian 
Thomas @manfromjupyter 
Martha @marthacryan 
Jason @jasongrout 
Tony @tonyfast
Isabela @isabela-pf 
Darian @afshin  
Alex @ajbozarth 

Happy new year!

Hooray for JupyterLab 3.0! Congrats and kudos who everyone who 
worked hard on it.

### What are people working on?
Go around the meeting area and ask.

- Martha
    - [#149](https://github.com/jupyterlab/lumino/pull/149) - 
    Realized I needed to add more to lumino and not jupyter lab 
    for the toggleable stuff
    - Tota11y toolbar (recommended by Thomas) is a potential tool 
    for testing this.
    - https://khan.github.io/tota11y/
    - How does a labeling something as a checkbox with ARIA roles 
    differ from using a true HTML checkbox? Using HTML as intended 
    usually works better, and screen readers will comment which 
    one it is.

- Tony
    - Needs help with setting up linked lumino JLab set up to test 
    the work around roles that need to be assigned in lumino.
    - Everytime you make a change in lumino, rebuild lumino before 
    JLab.
    - Going through [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491)
    - Interest in creating a binder that also reflects changes in 
    Lumino to help each other testing all these things.
    - Other times to pair program on this?

- Max
  - how to work on both lumino and JLab at once: https://github.com/jupyterlab/jupyterlab/blob/master/docs/source/developer/contributing.rst#testing-changes-to-external-packages
  - in progress lumino PR for ARIA roles for tabs: https://github.com/jupyterlab/lumino/pull/132
  - Martha may review?

- Thomas
    - Willing to provide support.
    - Posted https://github.com/jupyterlab/team-compass/issues/98#issuecomment-752748519 
    (thank you!)
    - If someone wants something to do that won’t step on other 
    people’s toes, lot of elements need either to be hidden or 
    revealed. Card: https://github.com/orgs/jupyterlab/projects/1#card-50646346 
    as part of #9399. I included a bunch of screenshots if you wanted to started working through it or section by section? https://imgur.com/a/6HvOcYK

- Isabela
    - WIP color contrast at [#8832](https://github.com/jupyterlab/jupyterlab/issues/8832) 
    and related PR [#9335](https://github.com/jupyterlab/jupyterlab/pull/9335). 
    Will help address sections of [#911](https://github.com/jupyterlab/jupyterlab/issues/911) 
    and [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399) 
    (since both note color contrast concerns).

- Jason: not actively working on something here specifically, but 
still available for questions and discussion

- Alex and Darian: not actively working on something here, but want 
to keep track and stay part of the discussion.

### What we need to work on
We need to take stock of what's being worked on and split up the 
work we know we need to do. 
- Here is [the project](https://github.com/orgs/jupyterlab/projects/1) 
for tracking accessibility (should have all issues and PRs we know 
of)(can be reorganized if we have different needs for sorting).
- First priorities include:
- [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491) 
This will make it possible to evaluate JupyterLab with a screenreader 
so we can both be aware of more problems and actually check that 
fixes are working.
- [#9399](https://github.com/jupyterlab/jupyterlab/issues/9399) 
(broken up into steps on the project, click on card to make issue 
when we are ready to work on it). WCAG 2.1 specifications.
- Editor? Is [#4878](https://github.com/jupyterlab/jupyterlab/issues/4878) 
a first priority right now?
- Right to left (RTL) language support?
    - We will likely be working in areas where these changes need 
    to be made for labeling reasons, so we may want to see if we 
    can include this support at the same time. Especially now that 
    we have RTL language transalations for JLab to test it with 
    (Gonzalo knows more). More info in issues [#3046](https://github.com/jupyterlab/jupyterlab/issues/3046) 
    and [#1163](https://github.com/jupyterlab/jupyterlab/issues/1163).

### Other Notes
- Feedback on accessibility event funding.
    - Update: Probably shouldn't rely on it. It's status isn't 
    certain with the pandemic.

## 01.27.21 Meeting Minutes
### Attendees
(oops! No one signed in today so I gave my best guess.)
Max @telamonian 
Thomas @manfromjupyter 
Martha @marthacryan 
Jason @jasongrout 
Tony @tonyfast
Alex @ajbozarth 
Karla @karlasupldaro
Isabela @isabela-pf 

### What are people working on?
- How is everyone doing?
    - Come up with different intro questions :upside_down_face: 
- Does it make sense to have these meeting notes documented 
outside an issue? I think there's enough content there that 
it's hard to navigate if you aren't just looking for the first 
or last comment.
    - Yes! Let's propose a place in the Jupyter accessibility repo.
- Can we make an issue about adding accessibility tests to the 
JupyterLab development process?
    - I was reminded by the discussion started on [JupyterLab 
    Classic #80](https://github.com/jtpio/jupyterlab-classic/issues/80).
    - I've also listed some existing tests. We should review 
    these to see if they could work or give us a baseline for 
    working with lumino or jupyterlab components.
         -  [squizlabs / HTML_CodeSniffer](https://github.com/squizlabs/HTML_CodeSniffer)
        - IBM's [accessibility-checker](https://www.npmjs.com/package/accessibility-checker)
        - [AccessLint / accesslint.js](https://github.com/AccessLint/accesslint.js) 
        - [pa11y / pa11y](https://github.com/pa11y/pa11y-ci)
        - [dequelabs / axe-core](https://github.com/dequelabs/axe-core)
- Should we also make an issue reminding us to make accessibility 
docs as we make all the WCAG and other changes?
- Check in! In the JLab team meeting, we have accessibility listed 
as an issue people are working on within the JLab 4.0 timeline. 
What scope do we want to report? Are we working on [#9339](https://github.com/jupyterlab/jupyterlab/issues/9399) 
and [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491) 
only right now, or is someone planning to work on the editor?
    - [#9339](https://github.com/jupyterlab/jupyterlab/issues/9399) 
    and [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491) 
    for sure. Editor changes are still being researched so mark it 
    as possible but uncertain.
- Max started working on [#9491](https://github.com/jupyterlab/jupyterlab/issues/9491)
    - Probably JupyterLab and not lumino level fixes. 
- Martha
    - [#9622](https://github.com/jupyterlab/jupyterlab/pull/9622) 
    blocked by small translation issue
    - Needs review or advice how to proceed.
    - Otherwise ready to merge (Thomas tested it!)
    - [#149](https://github.com/jupyterlab/lumino/pull/149) Merged!
- Tony
    - [#9648](https://github.com/jupyterlab/jupyterlab/pull/9648)
    - With Max's PR, this should cover #9491!
    - Tony's PR should cover all landmarks.
    - Only thing left is making it so screen readers can access 
    those different labels.
    - How does this interact with JLab themes? We need to test 
    what this PR means visually.

### Other Notes
- Spatial experience and vision
    - Thomas says you are generally not supposed to label things 
    that will be accessed via screen reader with left, right, 
    here, so on because it doesn't really mean anything to those 
    users.
    - In CSS classes or other areas not accessed by a screen 
    reader, this is okay. 
- Tab index convention 
    - Seems like the main recommendation is to set everything 
    to tabindex 0 (because it defaults to the browser).
    - Does this work for JupyterLab?
    - -1 means you aren't going to see it. For example a is a 
    tab and buttons are tabbed, so there is possibility for 
    things being tabbed twice. So sometimes -1 is to avoid 
    redundancy.
    - Tabs are only for people to jump to those regions. They 
    do not define the region or header/hierarchy. But tab puts 
    you in those places to then announce the region or header.

### Merged PRs (let's celebrate!)
- Martha merged [lumino #149](https://github.com/jupyterlab/lumino/pull/149)! :tada: 
- Max merged [lumino #150](https://github.com/jupyterlab/lumino/pull/150)! :confetti_ball:  
- Isabela merged [jupyterlab #9335](https://github.com/jupyterlab/jupyterlab/pull/9335)! :sunflower: 

### Next steps
- Isabela
    - Propose moving accessibility meeting notes to the 
    accessibility repo so they are easier to search.
    - Follow up on test/CI ideas
    - Update accessibility project with merged PRs
    - Start issue for adding accessibility page to docs
    - Add resources to contributing guidelines encouraging people 
    to read up on accessibility.
- Thomas
    - Will note the next five steps they recommend focusing on and 
    make relevant issues.
- Martha
    - Work on #9622
- Max 
    - Review Martha's #149 PR
    - Work on PR for #9491
- Tony
    - Continue on [#9648](https://github.com/jupyterlab/jupyterlab/pull/9648) 
    reviewing visual impact and with a JupyterLab-style class name.

## 02.10.21 Meeting minutes
### Attendees
- Max @telamonian 
- Tony @tonyfast 
- Alex @ajbozarth 
- Martha @marthacryan 
- Jason @jasongrout 
- Isabela @isabela-pf 
- Nick @bollwyvl 
- Thomas @manfromjupyter 

### What are people working on?

- Keyboard shortcuts and default keyboard navigation with assistive
 devices. This Came up with this PR JLab 
 [#9031](https://github.com/jupyterlab/jupyterlab/pull/9031) but it 
 seems like it could be a bigger discussion for understanding how 
 these things interact now and in the future.
    - Thanks to Thomas for replying here!

- Max has been working on a new filebrowser. Trying to bake 
accessibility in on a low level. Issue with notes:
  - https://github.com/jpmorganchase/regular-table/issues/114
  - Using the WAI ARIA spec for grid and table properties. These 
  not only need regular labels, but also descriptions for how they 
  are nested and a flag for the position.
  - Max would like feedback/for someone to test it with a screenreader.
  - This is a really helpful exploration that should help us with 
  other tables used in JupyterLab. Further references with a [treegrid 
  example](https://w3c.github.io/aria-practices/examples/treegrid/treegrid-1.html) 
  are here.

- Question on Max's [lumino PR](https://github.com/jupyterlab/lumino/pull/132) 
conflicts with https://github.com/jupyterlab/jupyterlab/pull/9622
    - Martha reviewed it and is clarifying what labels they are using 
    across PRs so that they are consistent.

- Martha's PR at [#9622](https://github.com/jupyterlab/jupyterlab/pull/9622) 
is ready for final review and to be merged after one more commit 
to match labels across PRs.

- Nick
  - For testing: pa11y -s, --standard <name> the accessibility 
  standard to use: Section508 (U.S. focused), WCAG2A, WCAG2AA 
  (default), WCAG2AAA – only used by htmlcs runner
  - numfocus GSoC team would be a solid team for working on 
  accessibility docs

### Other Notes
- Isabela opened 
    - [#9742](https://github.com/jupyterlab/jupyterlab/issues/9742) 
    because I've had some people asking me about accessibility tests 
    elsewhere and I wanted a place to collect the discussion as it 
    relates to JLab.
    - an issue on the accessibility repo about best practices for 
    [accessibility docs](https://github.com/jupyter/accessibility/issues/15)
- As a last check, remember to ask yourself if things need to be 
translated.
    - ARIA values usually need it
    - Table headers might need to be translated? This is worth 
    further research.
    - Data in a table does not need to be.
- Funding discussion
    - Possible Canadian grant: https://accessible.canada.ca/advancing-accessibility-standards-research/funding
    - NSF, NIH, DoE (both of them) NSF future of work https://www.nsf.gov/pubs/2021/nsf21548/nsf21548.htm
    - Does documentation seem like a good project to get outside 
    help on?
- Accessibility workshop updates! There isn't something we can 
share now, but people are working on it and there should be 
updates in the next few weeks.

### Merged PRs (let's celebrate!)
- Tony merged [#9648](https://github.com/jupyterlab/jupyterlab/issues/9648)! 
:tada: Thanks to Thomas, Martha, and Max for reviewing it! Congrats, all!

## 02.24.21 Meeting Minutes
### Attendees
- Jason Grout @jasongrout 
- Saul Shanabrook @saulshanabrook 
- Tony @tonyfast 
- Isabela @isabela-pf 
- Alex @ajbozarth 
- Max @telamonian 
- Martha @marthacryan 
- Adam @adpatter
- Thomas @manfromjupyter 
- And more!

### What are people working on?

- Isabela
    - Should I mention people for feedback on the [meeting minutes PR](https://github.com/jupyter/accessibility/pull/17)? It isn't urgent, but I don't know who would be good to ask.
- Tony
    - codemirror 6 talk about accessebility: http://bofh.nikhef.nl/events/FOSDEM/2021/D.javascript/codemirror.webm
    - tabindex was not that hard, but the rest is hard.
    - working on https://github.com/jupyterlab/jupyterlab/issues/9686 i am having a hard time understanding what happens to the focus on the sidebar.
        - look at https://github.com/jupyterlab/jupyterlab/pull/9622
    - it is an li with div's inside, replacing with anchors doesnt ever seem to find focus
    - linking setup example https://jupyterlab.readthedocs.io/en/latest/developer/contributing.html#testing-changes-to-external-packages
    - 
      - Probably should add a very concrete example of linking the Lumino packages to develop Lumino and test against JupyterLab
- Saul
    - Learning to code through working on JupyterLab accessability? Good first issues? 
        - currently organized issues https://github.com/orgs/jupyterlab/projects/1
        - Thomas's issues are a good (Thanks Thomas!)
        - This is the issue that covers what we need to do to be able to meet WCAG 2.1 standards. We are breaking it up into other issues to work on bit by bit as well (scroll to the bottom of the issue). https://github.com/jupyterlab/jupyterlab/issues/9399
- Max
  - possible scipy 2021 talk
    - talk notes: https://github.com/telamonian/tree-finder/tree/scipy-2021-talk-proposal/docs/scipy_2021
    - collaborators welcome
- Thomas
    - How can we support the work for tablists at [#9622](https://github.com/jupyterlab/jupyterlab/pull/9622)
    - Martha replies that that it needs to be rebased from Max's lumino PR and then it will be ready.
    - For the typescript gods, next priority imo for accessibility are the list items from this comment: https://github.com/jupyterlab/team-compass/issues/98#issuecomment-768800666

### Other notes
- Follow up on accessibility workshop status?
    - Having a meeting later today
- lumino + jlab dev notes: https://jupyterlab.readthedocs.io/en/latest/developer/contributing.html#testing-changes-to-external-packages
    - Saul was working on a binder here that links all lumino packages to juptyerlab: https://github.com/saulshanabrook/binder-jupyterlab-dev/blob/master/binder/postBuild
- setup an intermediate meeting for learning about accessibility and contributing to jupyterlab.

### Next Steps
- Set up binder to show lumino changes instanly for development testing. (Tony, Martha, maybe Max)
- Get merge rights for accessibility repo (Isabela)
- Gather a set of resources/guides to help start up our newcomers.(Isabela)
- Add specific example to lumino development docs that shows how to link it up to JupyterLab (?)
- Rebase #9622 to have it ready for review (Martha)
- Next week meeting to get people up to speed on accessibility efforts (Isabela, Tony, Saul)
- Review #9399 so you get context for what we are doing and we have a good place to start talking (Anyone trying to catch up on our current work)

## 03.10.21 Meeting Minutes

### Attendees
* Gonzalo
* Jason
* Q
* Saul
* Tony
* Nick
* Thomas
* Karla
* Martha
* Isabela

### What are people working on?
- Isabela
    - Looking into writing a CZI grant with the support of Tania and maybe Tony? Just an FYI. I will keep you updated.
    - Trying to write a roadmap of what we are doing that is not just a Github project or made of issues because people keep asking me what we are doing.
- Tony
    - nbconvert
        - nbconvert jinja templates are not accessible, they are just divs. If we made them header elements, then nbviewer will be accessbile
            - Thomas: Could make them accessible just with roles
            - nbiewer: https://nbviewer.jupyter.org/
            - For context nbviewer is a “notebook viewer”.
                - Ex:https://nbviewer.jupyter.org/github/ipython/ipython/blob/6.x/examples/IPython%20Kernel/Index.ipynb
                - It lets you view a jupyter notebook and send that link around
                - Github will also render jupyter notebooks, like it renders markdown. But it does a bad job of it, its very slow
            - Thomas: Why make them look good? Search engine optimization?
            - Nick: There is no SEO, all robots turned off. Its a way public notebooks can be shared
            - This could be a good first issue (because no typescript!)and it still imapcts the comunity.
    - binder for jupyterlab development making changes in lumino [jupyter/accessibility #20](https://github.com/jupyter/accessibility/pull/20).
- Thomas
    - Get all the low vision stuff in one place so people can start jumping into it
    - Ask Gonzalo a question to follow up on internationalization work and overlap with low vision/zoom support. Where are the packages
        
- Saul
    - A lot of this work seems to be focused on helping folks with vision problems. Have any of them come on this working call? Possibly related to grants, for paying people to help diagnose what the main problems are?
        - At least one person has. Many people don't necessarily disclose why they have the knowlegde they do for us, so I'm unsure.

- Martha
    - Needs to follow up on Max's lumino PR and move forward as much as she can with the related JupyterLab PR. :)

### Other notes
- Follow up on accessibility workshop meeting (two weeks ago)?
    - There should be an email this week following up with people who expressed interest in running workshops to check if they are still interested

### Next Steps
- Review [deathbeds/accessibility #4](https://github.com/deathbeds/accessibility/pull/4). (Isabela)
- Edit/update [jupyter/accessibility readme](https://github.com/jupyter/accessibility/pull/24) to have accurate information about these meetings. (Isabela)
- Get a roadmap draft ready for review (Isabela)
- Review [jupyter/accessibility #20](https://github.com/jupyter/accessibility/pull/20). (Isabela)
- Martha - finish review of Max's lumino PR so that the JL PR can be rebased off of that
    - Actually just took another look and approved
- Start funding/grant discussion for jupyter/accessibility to keep people updated and support other opportunities. (Isabela)
- Publish language packages that have full  localization so people can test them (Gonzalo)