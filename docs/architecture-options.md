# Architecture Options

## Recommendation: React Native + Expo + TypeScript

Best current fit for this project.

### Pros
- One codebase for Android and iOS
- Can also target web later
- Excellent speed for MVP work
- Large ecosystem
- Works well from Linux during early development
- iOS builds can be handled through Expo Application Services later

### Cons
- Native edge-cases sometimes need extra care
- Final App Store release steps are still more awkward without a Mac
- Some native integrations may eventually need cloud build or Mac access

## Option 2: Flutter

### Pros
- Strong cross-platform UI consistency
- Good performance
- Android/iOS/web from one codebase

### Cons
- Flutter is not installed here
- Heavier setup path on this tower right now
- Web story is fine, but for this type of product Expo/React Native is usually the more practical start

## Option 3: PWA-first web app

### Pros
- Simplest deployment path
- One product for browser users immediately
- No app-store gatekeeping to begin with

### Cons
- Weaker mobile-native experience
- iOS notifications/background capabilities are more limited
- Less ideal if the goal is a polished app-store app

## Practical conclusion
If the priority is to start building now, preserve the option of iOS and Android, and maybe add browser access later, React Native with Expo is the best balance.

## Suggested first-phase product shape
- Mobile-first app
- Shared React Native codebase
- Keep web compatibility in mind but do not let it slow MVP delivery
- Use backend and data model choices that can support web later
