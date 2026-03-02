# Aurora Block V1 – Gaps Filled
## Overview
This document completes the previously defined Aurora Block V1 architecture by filling the four implementation gaps:
1. Encoder / Embedding Layer
2. Span Boundary Detection
3. Domain Activation Logic
4. Interpretability Computation
These components transform Aurora from a conceptual model into an executable architecture capable of replacing transformer-based reasoning.
## 1. Encoder / Embedding Layer
Aurora requires an initial perception layer to convert surface text or event data into conceptual inputs. This encoder does NOT perform reasoning; it merely provides structured inputs.
Pipeline:
1. Use an off-the-shelf encoder (LLM or sentence transformer) for:
- event_embedding
- subject/verb/object parsing
- register, modality, polarity tags
2. Map referents to Roles:
- “I” → speaker role
- “we” → speaker + inferred group members
- named entities → lookup or create Role entries
3. Construct ConceptualEvent:
- parsed_subject, parsed_verb, parsed_objects
- speaker_role_id, addressee_role_ids
- event_embedding
- tags (tense, mood, politeness, etc.)
4. Initialize Role + Domain embeddings:
- Roles receive embeddings from encoder + type tags
- Domains receive embeddings tied to domain_type (e.g. “movement”, “conversation”)
## 2. Span Boundary Detection
Spans replace positional encoding and define conceptual episodes.
v1 Heuristics:
A new Span begins when ANY of the following occur:
- Topic similarity drops below threshold
- Speaker changes with domain shift
- Explicit boundary markers (“anyway”, “by the way”, scene change)
- Long temporal gaps
Algorithm:
if (time_gap > T_max)
or (topic_similarity < TOPIC_THRESHOLD)
or (explicit_marker_detected)
→ new span
else
→ continue current span
Upgrade path:
Train a span boundary classifier using:
- event_embedding sequence
- discourse markers
- pragmatic cues
## 3. Domain Activation Logic
Domains are meaning-fields activated by verbs, not by token proximity.
v1 Lexical Mapping:
Verbs select Domains:
Movement:
go, walk, run, travel, drive, fly
Conversation:
talk, ask, tell, explain, discuss
Planning/Intention:
want, plan, decide, hope, intend
Obligation (via mood/modality):
must, should, have to, require, forbid
Implementation:
function verbToDomainType(verb, tags):
if verb in MOVEMENT: return “movement”
if verb in CONVERSATION: return “conversation”
if verb in PLANNING: return “planning”
if tags.modality == “deontic”: return “obligation”
return “generic”
Upgrade path:
Train a classifier f(event_embedding) → domain_type.
## 4. Interpretability Computation
Interpretability replaces attention. It measures how aligned two Roles are within a Domain.
Interpretability is computed as:
I = (role-domain similarity + discourse evidence) * temporal_decay
Components:
1. Role-Domain Similarity
Project roles into domain-modulated space:
r_i_dom = f(role_embedding_i, domain_embedding)
Compute cosine similarity or learned metric.
2. Discourse Evidence
Adjust up for:
explicit agreement, shared planning signals
Adjust down for:
disagreement markers, contradiction
3. Temporal Decay
I *= exp(-λ * Δt) where Δt is time since last reinforcement.
Collapse Rule:
If I < THRESHOLD or Domain deactivates:
WE collapses (active = false)
Thresholds can vary by domain:
- conversation WE is fragile
- institutional WE is more stable
## 5. Integration into Aurora Block V1
These components integrate into existing AuroraBlockV1:
ensureSpan(state, event):
uses span boundary rules
activateOrReuseDomain(state, event, span):
uses verbToDomainType
updateDomainParticipants(state, domain, event):
assigns speaker + addressees
processWePrimitives(state, domain, span, event):
instantiates WE with appropriate type
updateAllWeInterpretability(state):
applies I(R1, R2 | Domain) computation
closeDeadStructures(state):
ends spans and domains appropriately
The block now functions end-to-end as a transformer replacement with:
- explicit episodes (Spans)
- contextual manifolds (Domains)
- agent-topology dynamics (Roles)
- relational operators (WE)
## Conclusion
With these four gaps filled, Aurora Block V1 is fully implementable.
The encoder handles perception,
Spans provide structural segmentation,
Domains structure meaning,
Interpretability drives conceptual dynamics,
and WE functions as a native operator inside the reasoning engine.
This specification is suitable for engineering implementation, patent continuation, and integration into the larger Aurora architecture.