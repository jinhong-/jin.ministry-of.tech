---
layout: post
title: Feature Flags is the new branching strategy
date: 2024-10-07 13:45:00 +0800
categories: []
---

With modern software engineering practices, we no longer lean into complex branching strategies to help us with feature gating, but rather feature flags. While traditional thinking leads us to believe that this increases risk due to the lack of isolation, it actually does the opposite in my experience for the following reasons
1. It creates a false sense of security to software engineers, leading them to believe that their codes will not impact production, hence there is less dilligence and more complacency
2. It makes codes extremely difficult to merge later on, as you end up with tons of merge conflicts and potential merge errors and issues, creating more bugs, and delays in releases
3. It creates unnecessarily complicated workflows, and confuses new joiners as it takes a significantly longer to explain how to correctly branch
4. It can make it difficult to apply specific rules or contraints to your repository due to the limitations of the source control you are using (GitHub, BitBucket, GitLab, etc)

This should set the precedent on my stance on complex branching strategies, as I am a firm believer of trunk based development

Feature flags are born out of necessity. As there are no silver bullets in software engineering, you cannot remove complex branching strategies without sacrificing something else. In this case it is the ability to isolate/prevent certain features from being released when they are not ready, hence we have feature flags to help with hiding specific features. This creates specific added benefits as side effects. This includes
1. A potential way to do A/B testing
2. Ability to "schedule" ahead of time when a feature should be "released"
3. Ability to "rollback", "block" or "disable" features due to a critical issue that needs to be resolved
4. Enable/Disable features for specific groups while maintaining the exact same code base, either as a private beta, or for internal testing, etc

Some tips on managing feature flags
1. Feature flags are a form of technical debt. Treat them as such. Ensure they always have a finite lifespan, and provide a deprecation/removal/sunset strategy for them
2. Avoid at all costs, having permanent feature flags. Do not use them to support things like different customer tiers, etc. If you have such needs, feature flags is not for you. Look elsewhere
3. I have found that feature flags are best implemented on the frontend where you have most information about the user. Generally speaking avoid having feature flags on the backend as they have lesser information about the user to work with to toggle features for. If you are experimenting with a new version of a feature, you are better off having an API versioning strategy that creates a new endpoint for your new version of the feature, then have your frontend consume feature flags to switch between both endpoints instead

Lastly, what platforms for feature flags are out there? Tons. What I would say is that you shoud look at your needs to decide what you want. Personally i prefer simpler, transparent costs and a super feature rich platform as the nature of the products I work on rely heavily on toggling it for specific environments, users, tenant, which some platforms do not offer the ability to have custom contexts to apply flags to. Also some platforms do offer the ability to detect "dead" flags, which can ease out on your flag removal strategy, which i mentioned is necessary as it is not meant for long time use. Here are some below that I have seen, and used
- PostHog
- ConfigCat
- Firebase Remote Config
- LaunchDarkly
- Optimizely
