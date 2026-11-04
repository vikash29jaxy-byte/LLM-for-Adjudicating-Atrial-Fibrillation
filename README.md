Supplementary Methods for:

"Performance of Local Large Language Models for Adjudicating Atrial Fibrillation Hospitalizations"
This repository contains the adjudication criteria, cohort derivation details, prompting strategies, and evaluation benchmark results used in the study.

Supplement

Atrial Fibrillation Hospitalization Adjudication Criteria

Guidance for Adjudicating Atrial Fibrillation Hospitalizations

Purpose
Determine whether atrial fibrillation (AF) was an active clinical problem requiring hospital-level management or materially contributing to the admission, using clinical judgment and the electronic health record narrative (supplemented by linked clinical context where specified). The core question is: Was atrial fibrillation an active clinical issue during this hospitalization, rather than solely a remote, historical, or incidental diagnosis?

How to Adjudicate

Label as “AF Hospitalization: YES” if:

In your clinical judgment, new, recurrent, worsening, or symptomatic AF contributed directly to the patient's presentation or admission.
AF required active inpatient management, such as pharmacologic rate control, rhythm control, electrical or chemical cardioversion, catheter ablation, acute anticoagulation initiation/decision-making, or close hemodynamic monitoring.

AF materially affected the patient's hospital course or clinical trajectory.

Common clinical phrases and presentations that support labeling as YES:

“Presented with palpitations and lightheadedness found to be in AF with rapid ventricular response (RVR).”
“Admitted for acute decompensated heart failure triggered by new-onset atrial fibrillation.”
“Initiated on IV diltiazem drip / amiodarone infusion for rate/rhythm control of AF.”
“Underwent successful direct current cardioversion (DCCV) during hospitalization.”
“Transitioned to oral anticoagulation following acute inpatient AF episode.”

Label as “AF Hospitalization: NO” if:

AF is documented solely as a remote past medical history entry or a static item on the problem list without acute relevance to this admission.
AF was stable, controlled on home medications, asymptomatic, and did not contribute to the hospital admission or require active acute interventions.
Tachycardia or symptoms are present but attributable to non-arrhythmic causes (e.g., sinus tachycardia secondary to sepsis or dehydration) without clinical or electrocardiographic documentation of AF.
Anticoagulation or rate-control agents are listed only as home medications or administered for an unrelated indication without active AF management.
The discharge summary lacks sufficient documentation to establish that AF was an active clinical problem during the stay.

Common examples that support labeling as NO:

“Admitted for elective total knee arthroplasty. Past history of chronic AF, rate-controlled on home apixaban and metoprolol.”
“Admitted for community-acquired pneumonia; sinus tachycardia noted on telemetry; history of paroxysmal AF mentioned but no recurrence.”
“Admission for GI bleed; anticoagulation held; no active AF or arrhythmias during stay.”

Prompting Strategies

System Instruction: All models were executed under strict deterministic inference constraints without chain-of-thought exposure "Use only the supplied deidentified MIMIC-IV record. Do not reveal reasoning. Return only YES or NO and no explanation."

1. Direct Prompt

Did this hospitalization involve atrial fibrillation as a documented active clinical problem? Do not count a remote history alone. Answer with a single word: YES or NO.

2. Role-Based Prompt

You are a board-certified cardiologist and clinical-trial endpoint adjudicator. Determine whether atrial fibrillation was an active clinical problem during this hospitalization, rather than only a remote or incidental historical diagnosis. Answer with a single word: YES or NO.

3. Structured Prompt

Adjudicate whether atrial fibrillation was an active problem during this hospitalization. 

Classify as YES when the discharge summary supports one or more of the following:
1. New, recurrent, worsening, or symptomatic atrial fibrillation contributed to presentation or admission; OR
2. Atrial fibrillation required active inpatient rate control, rhythm control, cardioversion, ablation, anticoagulation decision-making, or other hospital-level management; OR
3. Atrial fibrillation materially affected the hospital course.

Do not classify as YES for a remote history or stable problem-list mention alone. Do not infer AF from age, stroke, heart failure, anticoagulation, or tachycardia without documentation linking it to AF.

Answer with a single word: YES or NO.

4. Multimodal / Context-Fusion Prompt
Adjudicate whether atrial fibrillation was an active problem during this hospitalization. Use BOTH the discharge summary and the linked AF-management context supplied below. 

The linked context may include rate/rhythm-control drugs, anticoagulants, cardioversion, ablation, or electrophysiology procedures, but these are nonspecific and must be interpreted with the narrative. Do not count a remote history alone and do not infer AF from a medication by itself.

Answer with a single word: YES or NO.

--- LINKED AF MANAGEMENT CONTEXT ---
Medication Orders: {medication_context}
Procedures & Interventions: {procedure_context}
--- END LINKED CONTEXT ---

