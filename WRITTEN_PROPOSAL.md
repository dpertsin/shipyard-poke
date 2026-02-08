# Written Proposal - Poke App

**Submission Date:** February 2026
**App Name:** Poke - Beautiful Reminders
**Platform:** iOS & Android (React Native + Expo)
**Monetization Partner:** RevenueCat

---

## Executive Summary

Poke is a cross-platform reminder app built to solve a real problem faced by tech enthusiasts and phone reviewers: the inability to maintain reminders when switching between iOS and Android. With 100% offline functionality, custom snooze controls, powerful recurring reminders, and a beautiful user interface, Poke delivers features that no single competitor offers together.

Our freemium model provides unlimited local reminders for free, with a $2.99/month premium tier for cloud sync powered by RevenueCat. We're targeting the 600k subscribers of Sam Beckman (who inspired this app) and the broader cross-platform user community.

---

## The Problem

### Pain Points in the Reminder App Market

**1. Platform Lock-In**
The best reminder apps are platform-specific (Things 3 for iOS, TickTick struggles with iOS features). When users switch devices, they lose all their reminders or face hours of manual recreation.

**2. Feature Fragmentation**
No single app combines:
- Custom snooze from notifications (exact time, not just 5/15/30 min presets)
- Powerful recurring reminders (hourly, every N days, complex patterns)
- Proper cross-device sync (dismiss on one device, disappears everywhere)
- Beautiful, intuitive UI with smooth animations

**3. Forced Cloud Dependencies**
Most modern reminder apps require accounts even for local use, raising privacy concerns and creating barriers to adoption.

**4. Complexity vs. Power Trade-off**
Simple apps lack features (Apple Reminders), while powerful apps have steep learning curves (Todoist, Notion).

### Market Validation

**Sam Beckman's Challenge (December 2025)**
Tech YouTuber Sam Beckman (600k subscribers) challenged developers to build his perfect reminder app. His requirements matched exactly what's missing in the market:
1. Custom snoozing from notifications
2. Powerful recurring reminders
3. Proper cross-device sync
4. Beautiful UI

---

## The Solution: Poke

### Core Value Proposition

**"Beautiful reminders that actually work - across iOS and Android"**

Poke is a local-first reminder app with optional cloud sync, delivering four key features competitors don't combine:

### Feature Set

#### 1. Custom Snooze from Notifications ⏰
- Snooze for exact times via notification input
- No need to open the app
- Works directly from notification actions
- **Why it matters:** Users filming videos or in meetings can quickly snooze without unlocking their phone

#### 2. Powerful Recurring Reminders 🔄
- Hourly, daily, weekly, monthly, yearly intervals
- Custom patterns (every 3 days, every 8 hours, 2nd Tuesday of month)
- Full RFC 5545 RRULE support under the hood
- **Why it matters:** Real-world tasks (medication, plant watering, bill payments) don't fit simple daily/weekly patterns

#### 3. Proper Cross-Device Sync ☁️ (Premium)
- Dismiss on iPhone → disappears on Android tablet instantly
- No "ghost notifications" on old devices
- Conflict-free sync with operational transformation
- **Why it matters:** Users with multiple devices don't want to dismiss the same reminder 3 times

#### 4. Beautiful, Intuitive UI 🎨
- Playful font for friendliness
- Time-grouped views (Morning, Afternoon, Tonight)
- Smooth completion animations with haptic feedback
- Dark mode that actually looks good
- **Why it matters:** A reminder app you use 20+ times per day should be enjoyable to use

### Unique Differentiators

| Feature | Apple Reminders | Todoist | TickTick | Google Tasks | **Poke** |
|---------|----------------|---------|----------|--------------|----------|
| Cross-platform sync | ❌ iOS only | ✅ | ✅ | ✅ | ✅ |
| Custom snooze (exact time) | ❌ | ❌ | ❌ | ❌ | ✅ |
| Powerful recurring | ✅ | ✅ | ✅ | ❌ | ✅ |
| Offline-first (no account) | ✅ | ❌ | ❌ | ❌ | ✅ |
| Beautiful UI | ✅ | ⚠️ Dated | ✅ | ⚠️ Basic | ✅ |

---

## Target Audience

### Primary Personas

**1. The Platform Switcher (35% of market)**
- **Profile:** 25-40 years old, tech-savvy professional
- **Pain:** Rebuilds reminders every 6-12 months when switching phones
- **Motivation:** Wants seamless experience across devices
- **Example:** Sarah, 32, product manager who uses iPhone for work, Android for personal

**2. The Phone Reviewer (5% of market, high influence)**
- **Profile:** YouTubers, bloggers, tech journalists
- **Pain:** Switches devices weekly, impossible to maintain reminder consistency
- **Motivation:** Needs reliable system despite constant device changes
- **Example:** Tech YouTuber with 500K subscribers who uses 4+ phones monthly

**3. The Privacy-Conscious User (25% of market)**
- **Profile:** 30-50 years old, values data ownership
- **Pain:** Doesn't trust cloud-based apps with personal data
- **Motivation:** Wants full control over data, offline functionality
- **Example:** Alex, 38, software engineer who prefers local-first apps

**4. The Power User (20% of market)**
- **Profile:** 25-45 years old, uses reminders for everything
- **Pain:** Current apps lack features (custom snooze, complex recurring)
- **Motivation:** Needs advanced features without complexity
- **Example:** Jamie, 29, freelancer with 50+ active reminders

**5. The Casual Organizer (15% of market)**
- **Profile:** 18-35 years old, wants simple task management
- **Pain:** Current apps too complex or ugly
- **Motivation:** Needs something that "just works" and looks good
- **Example:** Mike, 24, student who wants to remember assignments and chores

### Market Size

- **TAM (Total Addressable Market):** 500M smartphone users who use reminder apps
- **SAM (Serviceable Addressable Market):** 50M cross-platform users
- **SOM (Serviceable Obtainable Market):** 500K users in Year 1

**Revenue Projections (Conservative):**
- Year 1: 10,000 premium users × $2.99/month = $359,000 annual revenue
- Year 2: 50,000 premium users × $2.99/month = $1,795,000 annual revenue
- Year 3: 150,000 premium users × $2.99/month = $5,385,000 annual revenue

*(Assumes 2% free-to-paid conversion rate, industry average for productivity apps)*

---

## Monetization Strategy

### Freemium Model: Local Free, Sync Premium

#### Free Tier (Local-Only)
**What's included:**
- ✅ Unlimited reminders
- ✅ All features (recurring, snooze, lists, tags, subtasks)
- ✅ No account required
- ✅ No ads, ever
- ✅ No artificial limits

**Why free tier is generous:**
1. **Lower barrier to entry** - Users try before they commit
2. **Word-of-mouth growth** - Free users become advocates
3. **Privacy appeal** - "Use it forever without giving us data"
4. **Platform for premium** - Once users rely on Poke, they want sync

#### Premium Tier: Poke Pro ($2.99/month)
**What's included:**
- ✅ Cloud sync across unlimited devices
- ✅ Dismiss on one device, disappears everywhere
- ✅ Automatic backup
- ✅ Priority support

**Why $2.99/month:**
- **Lower than competitors** - Todoist ($4/mo), TickTick ($3.49/mo)
- **Low commitment** - One coffee per month
- **High perceived value** - Users see sync as essential once they have multiple devices

**Annual option:** $29.99/year (17% discount)

### Revenue Streams

**Primary: Subscriptions (95% of revenue)**
- Monthly: $2.99
- Annual: $29.99
- Managed entirely through RevenueCat

**Secondary: Future Opportunities (5%)**
- Team/family plans ($9.99/month for 5 users)
- Lifetime license ($99.99 one-time)
- Enterprise licensing (custom pricing)

### Why RevenueCat?

**1. Cross-Platform Subscription Hell**
Without RevenueCat:
- Implement StoreKit 2 (iOS)
- Implement Google Play Billing 6 (Android)
- Build receipt validation server
- Handle subscription status webhooks
- Manage cross-platform purchase restoration
- Track subscriber analytics manually

**Estimated time:** 4-6 weeks

With RevenueCat:
- Single SDK for both platforms
- Receipt validation handled
- Webhooks abstracted
- Purchase restoration works cross-platform
- Built-in analytics dashboard

**Actual time:** 2-3 days

**2. Business Benefits**
- **Faster to market** - Launch 4 weeks earlier
- **Reduced maintenance** - No payment infrastructure to maintain
- **Better analytics** - See MRR, churn, LTV out of the box
- **A/B testing** - Test pricing and offerings
- **Global compliance** - RevenueCat handles App Store/Play Store rules

**3. Cost Justification**
- RevenueCat: 1% of tracked revenue (after $2,500/month free tier)
- Alternative: $5,000-$10,000 to build + ongoing maintenance
- **ROI:** Positive after 100-200 subscribers

---

## Go-to-Market Strategy

### Phase 1: Beta Launch (Month 1)
- Internal testing (50 users)
- TestFlight + Google Play Internal Testing
- Gather feedback, fix critical bugs
- **Goal:** 500 active beta users

### Phase 2: Public Launch (Month 2)
- Submit to App Store and Google Play
- Launch Product Hunt campaign
- Post on Reddit (r/Android, r/iOS, r/productivity)
- Email MrWhosetheBoss (app inspired by his challenge)
- **Goal:** 5,000 downloads, 100 premium subscribers

### Phase 3: Influencer Outreach (Month 3-6)
- Sponsor tech YouTube channels
- Partner with productivity bloggers
- Cross-promote with complementary apps
- **Goal:** 50,000 users, 1,000 premium subscribers

### Phase 4: Content Marketing (Month 6-12)
- Blog posts on productivity, app development
- YouTube tutorials on using Poke
- Case studies from power users
- **Goal:** 200,000 users, 4,000 premium subscribers

### Viral Coefficient Target
- **K-factor:** 0.3 (every user brings 0.3 new users)
- **Mechanism:** "Invite friends to sync" referral program (Year 2)

---

## Competitive Advantage

### Why Poke Will Win

**1. Feature Combination**
We're the only app with all four key features together. Competitors excel at 1-2 areas but compromise elsewhere.

**2. Local-First Philosophy**
Privacy-conscious users choose us because data stays on device. When they want sync, we're already their trusted app.

**3. Cross-Platform Parity**
Built with React Native - identical experience on iOS and Android. Competitors often favor one platform.

**4. Developer Experience**
Open-sourcing the codebase (Year 2) builds community and trust, differentiating from closed-source competitors.

**5. Niche Focus**
We're laser-focused on cross-platform users, a underserved 50M+ market segment.

---

## Traction to Date

- ✅ **MVP built** - Full feature set implemented
- ✅ **Beta ready** - App ready for TestFlight/Play Internal Testing
- ✅ **RevenueCat integrated** - Subscription flow working
- ✅ **Supabase backend** - Cloud sync infrastructure ready

**Next Milestones:**
- Week 1: Beta launch (50 testers)
- Week 4: Public launch (App Store + Google Play)
- Week 8: 5,000 users, 100 paid subscribers
- Week 12: Featured on Product Hunt, 20,000 users

---

## Why This Matters

### Impact

**For Users:**
Poke gives back time. No more rebuilding reminders when switching devices. No more missed tasks because an app doesn't sync properly. Just a beautiful, reliable reminder system that works everywhere.

**For the Market:**
Poke proves freemium can work for productivity apps. Generous free tier builds trust; essential paid feature (sync) converts when users are ready.

**For RevenueCat:**
Poke demonstrates RevenueCat's value for indie developers. One developer, two platforms, subscription revenue from day one - without building payment infrastructure.

---

## Ask

We're seeking:
- ✅ **RevenueCat Partnership/Grant** - To offset initial costs and accelerate growth
- ✅ **Co-Marketing Opportunities** - Case study, blog post, or webinar featuring Poke

**What we offer:**
- Transparent metrics sharing
- Public case study on using RevenueCat
- Feedback on SDK/dashboard improvements
- Ambassador for indie developer community

---

## Appendix

### Links
- **Demo Video:** [YouTube link]
- **TestFlight:** [TestFlight link]
- **Google Play Internal:** [Play Console link]
- **GitHub:** [To be released]

### Contact
- **Email:** dpertsin@gmail.com
- **X:** [@dpertsin](https://x.com/dpertsin)
- **Linkedin:** [@dpertsin](https://www.linkedin.com/in/dpertsin/)
- **Github:** [@dpertsin](https://github.com/dpertsin)

---

**Prepared by:** Dimitrios Pertsinidis
**Date:** 9th February 2026
**Version:** 1.0.0
