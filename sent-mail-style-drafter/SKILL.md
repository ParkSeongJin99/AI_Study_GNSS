---
name: sent-mail-style-drafter
description: gmail-based email drafting that searches the user's sent mail for prior examples and creates a new gmail draft in the user's established style. use when the user asks to write, draft, compose, prepare, or create an email to someone, especially in korean academic, lab, administrative, professor, external institution, scheduling, request, apology, thank-you, submission, notice, or follow-up contexts. before drafting, find two sent emails to the same recipient group and two sent emails with similar purpose/content when possible, then match naming, subject length, paragraph count, nuance, and sign-off conventions.
---

# Sent Mail Style Drafter

## Core behavior

Create Gmail drafts in the user's own prior email style. Do not merely write a generic email. First search Gmail sent mail for style evidence, then draft the new email and save it as a Gmail draft.

Use this workflow when the user asks for an email such as:
- "연구실 구성원들에게 긴급 여름 워크숍 공지를 지메일 초안으로 작성해줘."
- "맹주현 박사님께 특허 관련 진행사항 내부미팅을 진행하고 싶다는 메일을 송부하고 싶어."
- "교수님께 서명 요청 메일 작성해줘."
- "행정실에 제출 일정 문의 메일 초안 만들어줘."

## Required workflow

1. Parse the user's request.
   - Identify recipient or recipient group, relationship category, purpose, required facts, urgency, and whether a specific recipient email address is available.
   - If the recipient email address is not explicitly provided, use Google Contacts or Gmail search when helpful to infer it. If still uncertain, create a draft only when the recipient field can be left safely blank or ask for the address.

2. Search sent mail before drafting.
   - Find **two sent emails to the same recipient group** when possible.
     - Examples of recipient groups: professor/senior academic, research-lab members, external institution, administrative office, collaborator/researcher, student group.
     - Search by exact recipient name/email first when known, then by group terms or similar addressee conventions.
   - Find **two sent emails with similar purpose/content** when possible.
     - Examples of purposes: notice/announcement, meeting request, signature request, document submission, schedule coordination, apology/understanding request, thank-you, follow-up, status update.
   - Read the selected examples. Use their style as evidence, not as content to copy.

3. Extract style signals from the examples.
   - Addressee naming: e.g., "교수님께", "연구원님들께", "연구실 구성원분들께", "안녕하세요 교수님,".
   - Subject length and structure: short noun phrase vs. full sentence; inclusion of bracketed labels; level of specificity.
   - Paragraph count and density: number of short paragraphs, whether bullet-like date/place lines are used, whether closing is separated.
   - Nuance: directness, politeness, degree of apology/양해, formality, whether the user tends to state purpose immediately.
   - Sign-off convention.

4. Draft the new email.
   - Preserve the user's factual request exactly. Do not invent dates, locations, attendees, attachments, deadlines, or institutional details.
   - If important facts are missing but the user asked for a draft, write a usable draft with neutral placeholders only when unavoidable.
   - Keep Korean academic/lab email style concise and natural.
   - Do not include analysis or style notes inside the email body.

5. Apply sign-off rules.
   - Use **"박성진 올림"** for professors and clearly superior academic/senior recipients.
   - Use **"박성진 드림"** for lab members, external institutions, administrative offices, researchers, students, and general professional recipients.
   - If the user's sent-mail examples strongly show a different convention for the exact recipient, follow the examples unless it conflicts with the professor/superior rule.

6. Create the Gmail draft.
   - Use `create_draft` for a new email.
   - Use a reply draft only when the user explicitly asks to reply to an existing thread or the request is clearly a response to a specific email.
   - Do not send the email unless the user explicitly asks to send it now after reviewing or approving the draft.

7. Report succinctly.
   - Tell the user that the Gmail draft was created.
   - Include the subject and the final body in the response so the user can review it.
   - Do not expose internal Gmail message IDs.

## Search strategy

Use Gmail search operators aggressively and adapt to the request.

For recipient-group examples:
- Exact recipient known: search sent mail with `to:<email>` or the recipient name.
- Professor/senior academic: search sent mail for terms such as `교수님`, `올림`, `서명`, `면담`, `여쭙`, `찾아뵙`.
- Lab announcement: search sent mail for `연구실`, `구성원`, `공지`, `안내`, `참석`, `회의`, `워크숍`, `스터디`.
- External institution/admin: search sent mail for `행정`, `제출`, `문의`, `요청`, `확인`, `드림`.
- Research collaborator/researcher: search sent mail for the person name/title plus `미팅`, `진행`, `논의`, `일정`, `공유`.

For similar-purpose examples:
- Notice/announcement: `공지 OR 안내 OR 송부 OR 공유`.
- Meeting request: `미팅 OR 회의 OR 논의 OR 일정 OR 가능하신`.
- Signature/request: `서명 OR 인준지 OR 날인 OR 요청 OR 여쭙`.
- Document submission: `자료 OR pdf OR 보고서 OR 제출 OR 송부`.
- Apology/understanding: `양해 OR 죄송 OR 사과 OR 불편`.
- Thank-you: `감사 OR 도움 OR 시간 내주셔서`.

If four good examples cannot be found, proceed with the best available evidence and state briefly that fewer examples were available. Do not fabricate example evidence.

## Drafting rules

- Prefer a short subject line unless prior examples show otherwise.
- Use natural Korean honorifics and avoid over-explaining.
- Keep the opening direct: brief greeting, self-introduction only when the recipient may not know the user or prior examples include it.
- For announcements, use a clear structure: greeting, reason/announcement, key details, request for understanding/action, closing.
- For meeting requests, use a clear structure: greeting, reason, proposed topic, request for availability or meeting, closing.
- For professor/senior requests, soften with forms such as "여쭙고자", "가능하실지", "편하신 시간", "감사드립니다".
- For lab/internal notices, be polite but operational: "안내드립니다", "확인 부탁드립니다", "양해 부탁드립니다".
- For external/admin mail, be polite and specific: include affiliation if useful and ask for confirmation/action clearly.

## Gmail tool usage

- Use Gmail `search_emails` or `search_email_ids` to locate candidate sent emails.
- Use `batch_read_email` to inspect the bodies of selected examples before drafting.
- Use `create_draft` to save the final draft.
- Use Google Contacts only to resolve recipient addresses when names are ambiguous or the user omits the email address.
- Never use `send_email` unless the user explicitly requests immediate sending.
