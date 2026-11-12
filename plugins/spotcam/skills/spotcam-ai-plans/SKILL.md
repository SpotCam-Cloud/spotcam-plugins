---
name: spotcam-ai-plans
description: Use when the user asks which SpotCam AI detection plan they need, what a camera can detect, what a plan includes or costs, or wants a camera to detect something (people, pets, cars, a baby crying, someone falling, a line being crossed, …) — e.g. "which AI plan should I get for the baby room?", "can my doorbell tell cars from people?", "我想知道有沒有陌生人進來，要訂什麼？".
---

# Choosing SpotCam AI plans

SpotCam sells AI detection plans per camera; a camera can hold several at
once. The `spotcam` MCP server lists the plans; **you** work out which ones
fit what the user wants. The server never recommends anything, and nothing is
subscribed unless the user explicitly chooses.

## 1. Understand the need

Ask only what you cannot tell already:

- **Which camera.** Call `list_cameras` and match the camera the user means by
  name; ask if several could match. Only cameras the user **owns**
  (`relation: owner`) can take plans.
- **What should it notice.** Turn the user's words into the capabilities that
  plans list under `includes`:

  | The user says | Capability |
  |---|---|
  | people, strangers, intruders | `person` |
  | someone they know vs a stranger | `face_recognition` |
  | cats, dogs | `pet` |
  | barking, meowing | `pet_sound` |
  | cars, scooters, someone parking | `vehicle` |
  | someone crossing a line, entering an area | `line_crossing` |
  | an item taken away (bag, parcel, bike) | `missing_object` |
  | bears, boars, monkeys, wild animals | `large_animal` |
  | a baby crying | `baby_cry` |
  | the baby's face is covered, the baby rolled over | `covered_face` |
  | glass breaking, screams, unusual noise | `abnormal_sound` |
  | an automatic album / time-lapse of the baby or the pet | `baby_diary` / `pet_diary` |
  | an elderly person fell and does not get up | `fall` |
  | sleep quality | `sleep_quality` |
  | a seat or space is taken too long | `occupancy` |
  | shoplifting | `theft` |

  If the request is vague ("keep an eye on the house"), ask one short
  question about the situation (indoor or outdoor, pets, children, a shop)
  instead of guessing.

## 2. Get the plans for that camera

Call `list_plans` with the camera's `sn`. Each plan has:

- `includes` — what it provides. A bundle includes several capabilities.
- `on_sale` — `false` means SpotCam does not sell it yet.
- `subscribed` — the camera already has it.
- `conflicts_with` — plan ids it cannot be held together with (a bundle and
  its own single plans; the indoor and outdoor packs).
- `free_trial_available` — the camera can still try it free for 7 days.
- `monthly` / `yearly` prices in USD and TWD.

If `firmware_update_needed` is true, tell the user to update the camera's
firmware in the SpotCam app first, and stop there.

## 3. Compose the options

1. Drop the needs a `subscribed` plan already covers, and tell the user they
   already have them.
2. For each remaining need, find the `on_sale` plans whose `includes` has it.
   If none, say plainly that this camera does not offer it (or that it is not
   on sale yet, when only an `on_sale: false` plan has it). Do not suggest
   another product.
3. Build the combinations of on-sale plans that cover every remaining need,
   leaving out any plan that `conflicts_with` a subscribed plan or with another
   plan in the same combination. Keep only combinations where every plan is
   needed.
4. Add up the prices. A bundle often costs less than its single plans and
   brings extra capabilities; mention those extras, but do not count them as a
   reason to pay more.
5. Show at most three options, cheapest first, in the user's currency
   (TWD for users in Taiwan, otherwise USD), monthly and yearly, and note which
   plans have a free trial.

Keep it factual: no urgency, no upselling, no plan the user did not ask about.

## 4. Only if the user chooses

`subscribe_plan` (one call per plan, with `sn`, `pid` and `monthly` or
`yearly`) records a subscription **request**; during the current test phase
nothing is charged. Call it only after the user picked the option and the
billing period in this conversation, and tell them what was recorded. For
anything else (orders, invoices, cancelling) point them to `manage_url` or
the SpotCam app.

If `list_plans` or `subscribe_plan` is not available, the user's AI client
does not offer plan tools; point them to the SpotCam website or app.
