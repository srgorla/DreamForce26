# Dreamforce 2026 Review: What We Tried and What Our Team Could Explore

Suggested presenter outline for a 35-minute review and 5-minute discussion.
Assumes a mixed audience of Salesforce developers, admins, and team leads.
Based on the workshop notes and screenshots in this repository; this is not a
verification of current product availability, licensing, or production readiness.

## Recommendations for the original notes

The original [Dreamforce26Review.Md](Dreamforce26Review.Md) remains unchanged.

| Recommendation | Why it helps |
| --- | --- |
| Start with three takeaways and a clear purpose | Gives the audience a reason to follow the demos. |
| Explain the user, problem, observed result, and team relevance for each example | Turns a screenshot collection into a story. |
| Show one or two result screenshots per topic | Keeps the presentation readable; setup details can support questions later. |
| Separate Ask and Grid within the Coworker section | The combined heading does not explain what each screenshot demonstrates. |
| Rename the coding section to “Salesforce tools through an AI client / MCP” unless you show an actual code change | The inspected screenshot shows record queries and a generated document, not code generation. |
| Treat “setup in less than 30 minutes” as a workshop observation, if measured | A prepared training org is different from a team's implementation effort. |
| Prepare evidence for governance, vulnerability remediation, and multi-agent orchestration | Their demo outlines below still need actual workshop results and screenshots. |
| Finish with one proposed experiment and a success measure | Gives the team something concrete to discuss. |

### Specific presentation fixes to consider

- The Casey live-test image link is split by the Help Portal section. Its intact
  form is `![Casey live test](screenshots/HelpAgent_Casey_Setup_LiveTest.png)`.
- Use one `#` title and `##` topic headings; use descriptive image captions
  instead of `alt text`.
- Use “Service Assistant — Dynamic Plans” consistently with the exercise guide.
- Keep org usernames and the plaintext training password out of the audience
  version. The original contains a password; remove it before sharing that file.
- Describe only the clients actually demonstrated. The current list mixes coding
  tools and collaboration apps without explaining their roles or connections.
- Add the student and exercise guide links to each workshop's reference page.
  The Service Assistant [guide reference](workshops/service-assistant-dynamic-plans/README.md)
  is already available.

## Suggested agenda

| Time | Segment |
| --- | --- |
| 0–2 min | Purpose and takeaways |
| 2–7 min | Coworker: Ask and Grid |
| 7–12 min | Casey: knowledge-based help |
| 12–18 min | Service Assistant: guided case resolution |
| 18–22 min | Salesforce tools through an AI client / MCP |
| 22–24 min | Data 360 governance and masking |
| 24–28 min | Salesforce vulnerability remediation |
| 28–32 min | Multi-agent orchestration |
| 32–35 min | Proposed experiment and takeaways |
| 35–40 min | Team discussion |

## Opening: three takeaways

Suggested opening:

> I explored several Salesforce workshops and captured the results. Today I’ll
> focus on what the demos actually showed, where they might fit our work, and
> what we would still need to validate in our own environment.

1. Natural-language requests can provide a useful way to explore Salesforce data.
2. Knowledge answers and guided case resolution address different service needs.
3. The useful evaluation is whether a workflow produces a correct, reviewable
   result with our data—not just whether the setup is quick.

## 1. Coworker: Ask and Grid

**Problem to introduce:** Finding a relevant record can require knowing the
object, filters, and navigation path in advance.

**Observed example:** A user asks whether there are gift certificates. The
captured response locates a record and identifies missing values and dates.

![Ask response locating a gift certificate and identifying missing fields](screenshots/Coworker_Ask2.png)

**Talk track:** Point out the question, the record link, and the missing-field
observations. Discuss how you would check the answer against the source record.
This example is useful for discussing data quality as well as record discovery.

**Team question:** Which recurring lookup or summary request would be worth
testing with our own representative data?

**Grid follow-up:** Show the [Grid screenshot](screenshots/AgentforceGrid.png)
only after explaining the task you performed in it and the resulting benefit.
Do not assume the audience knows how Grid differs from Ask.

## 2. Casey: knowledge-based help

**Problem to introduce:** Users repeatedly ask questions whose answers are
already documented, but finding the right document takes effort.

**Demo sequence:** Name the source document, show one question, show the answer,
then compare the answer with that source. If the demo displays citations, point
to them. Include an unanswered question to discuss what should happen next.

![Casey help-agent test captured during the workshop](screenshots/HelpAgent_Casey_Test.png)

**Suggested framing:** “The workshop explored answering help questions using
provided content. For our team, I would test this against a small, maintained
FAQ set before considering a wider rollout.”

**Team question:** Who would own the source content and review answers when a
policy changes?

Keep the [live-test screenshot](screenshots/HelpAgent_Casey_Setup_LiveTest.png)
as a fallback if the training site is unavailable. Confirm the site works before
offering a live demo.

## 3. Service Assistant: Dynamic Plans

**Problem to introduce:** A service representative needs to gather context,
follow policy, and decide which step comes next when resolving a case.

**Observed example:** The case screenshot shows an order-refund request with a
generated service plan containing suggested resolution steps.

![Order-refund case with a generated Service Assistant plan](screenshots/ServiceAssistantDynamicPlansTest1.png)

**Talk track:** Start with the case request, then walk through the suggested
steps. Explain which steps require the representative's judgment and which
actions were actually executed during your test.

**Evidence boundary:** This screenshot demonstrates a generated plan. It does
not by itself establish that a refund was processed or the case was resolved.
Use subsequent screenshots or record changes to support those claims.

**Workshop reflection:** The exercise calls for identity verification before
order retrieval. The visible plan starts with order retrieval. Explain whether
identity verification happened earlier; otherwise, use this as an example of
why generated plans need evaluation against the intended process.

**Team question:** Which repetitive case type has clear enough policies and
actions to support a small evaluation?

## 4. Salesforce tools through an AI client / MCP

**Problem to introduce:** A user working in another tool needs Salesforce
context to complete a task.

**Observed example:** The playground screenshot shows a Salesforce query,
returned case records, and a PDF document card in the conversation.

![AI playground showing a Salesforce query response and case-summary PDF card](<screenshots/Coding Agent with AIforce_Playground3.png>)

**Talk track:** Follow the request to the tool call, inspect the returned
records, then show the resulting document. Open the PDF if you want to claim
that its contents were validated; the card alone establishes only what the UI
displayed.

**Team question:** Where would this save a repeated context switch in our work?

Keep [connection setup](<screenshots/Coding Agent with AIforce_MCPClient.png>)
and the other playground screenshots for technical questions. If the audience
is mostly developers, give this segment more time and include one actual code
change with its validation result, if you have one.

## 5. Data 360 governance and masking

**Problem to introduce:** Different users may need different views of the same
data. A useful demo makes the effect of a configured privacy rule visible.

**Suggested walkthrough:** Choose one field from the workshop, explain its rule,
and compare the before/after result under the relevant access contexts. State
where the rule applies rather than implying it masks that field everywhere.

**Evidence to add:** The configured rule, the access context used for each test,
and a screenshot of the resulting field display. These results are not yet
documented in the original notes.

**Team question:** Which data should remain useful for a workflow while being
restricted for a particular audience?

## 6. Fix Salesforce vulnerabilities

**Problem to introduce:** Identifying a code issue is only the beginning; the
team needs to understand its impact, review the fix, and verify the result.

**Suggested opening:** “For this demo, I’ll follow one workshop finding from
detection through remediation and validation.”

**Demo sequence:**

1. Show one actual finding from the workshop and the affected code. Explain
   what triggered it and why it matters in that example.
2. Show the proposed correction as a small before/after diff. Explain the
   behavior it changes and identify any parts that still need human review.
3. Run the relevant check again and show its result. Also show the applicable
   functional test so the audience can see whether expected behavior remains.
4. Close with what the evidence establishes and any remaining findings.

**Talk track:** Keep the focus on one finding. Walk from the reported issue to
the code change and the validation result; avoid spending the segment navigating
setup screens or presenting an unexplained list of warnings.

**Evidence to add:** A screenshot of the original finding, the reviewed code
diff, and the follow-up check/test output. The original notes contain a workshop
reference but no finding or remediation result, so this is a proposed demo
sequence rather than a claim that a vulnerability has been fixed.

**Takeaway:** “An AI-proposed fix becomes useful when we can explain the change
and demonstrate that the relevant checks pass.”

**Team question:** Where could this fit into our existing code-review workflow,
and who would decide whether a suggested correction is appropriate?

## 7. Multi-agent orchestration

**Problem to introduce:** Some workflows involve several distinct responsibilities.
The demo should show why dividing them between agents helps with a specific task.

**Suggested opening:** “I’ll show one request, the responsibilities assigned to
each agent, and the evidence that the handoffs produced the intended result.”

**Demo sequence:**

1. Introduce the actual workshop scenario and its expected outcome. Name the
   participating agents and give each a one-sentence responsibility.
2. Submit the request through the demonstrated entry point.
3. Show a trace or other available execution evidence of the first handoff:
   which agent delegated, what context it passed, and what result came back.
4. Follow the result to the final response or record change. Distinguish an
   agent-to-agent handoff from an ordinary tool call.
5. If the workshop supports it, show one incomplete handoff or unavailable
   dependency and explain the observed recovery or escalation behavior.

**Talk track:** Spend more time on the boundaries between responsibilities than
on agent names. Explain how the final result incorporates the delegated work
and how someone investigating a failure would identify the relevant step.

**Evidence to add:** A diagram using the workshop's actual agent names, a trace
showing the handoff, and the resulting output. The current notes do not identify
the agents or prove an orchestration outcome; fill these in from the workshop
before presenting the outline as a completed demonstration.

**Takeaway:** “The value comes from clear responsibilities and reliable handoffs.
We should be able to explain why this workflow benefits from more than one agent.”

**Team question:** Do we have a workflow with distinct responsibilities that
would justify multiple agents, or would one agent with tools be sufficient?

## Closing: choose one experiment

Suggested closing:

> My proposal is to choose one recurring task, test it with representative data,
> and compare the results with how we handle it today. Which example is closest
> to a problem our team already wants to solve?

| Candidate experiment | Measure to agree before starting |
| --- | --- |
| Internal knowledge Q&A | Correct and source-supported answers on an agreed question set; appropriate handling of unanswered questions. |
| Case-plan assistance | Required-step coverage, incorrect suggestions, and representative effort compared with the current process. |
| Record lookup and summary | Correct records retrieved, factual accuracy, and time to produce a reviewed summary. |
| AI-assisted vulnerability remediation | Findings correctly addressed, follow-up check results, and human review effort. |
| Multi-agent workflow | Correct final outcomes, successful handoffs, and observable recovery from a failed step. |

Choose an owner, a small test set, and a review date. Treat benefits as hypotheses
until the team has measured them.

## Presenter preparation

- Rehearse the main path once and keep screenshots ready if a demo org expires.
- Add a one-sentence caption or takeaway to each screenshot you plan to show.
- Check image readability at presentation size; focus on the relevant panel.
- Distinguish workshop observations, documented capabilities, and ideas for our
  team. Confirm availability and licensing separately if those questions arise.
- Decide which result you want the audience to remember from each example.

For a shorter 15-minute review, present Coworker, Casey, and Service Assistant;
move the AI-client, governance, vulnerability, and orchestration demos to a
follow-up session.
