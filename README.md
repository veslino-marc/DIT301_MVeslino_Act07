# DIT3-1-MarcVeslino-Act07

## 1. What I Learned About Fragments and Navigation Components?

Fragments are reusable UI modules that can be added or removed without restarting the activity. In this project, I created three fragments (HomeFragment, ProfileFragment, and SettingsFragment) that each maintain their own lifecycle and views. Using ViewBinding ensures type-safe access to views, making the code safer and less error-prone.

The Navigation Component simplifies switching between fragments by centralizing all navigation logic in a single `nav_graph.xml` file instead of writing complex fragment transactions manually. The `setupWithNavController()` method automatically connects the BottomNavigationView to the navigation graph, so clicking a menu item automatically loads the correct fragment. This approach also handles the back button behavior automatically without extra code.

## 2. How did you make your UI adaptive to screen size or orientation?

I created separate layout files using Android's resource qualifier system:

- `layout/` folder - Default layouts for phones in portrait mode
- `layout-sw600dp/` folder - Larger layouts for tablets (screens 600dp or wider)
- `layout-land/` folder - Optimized layouts for landscape orientation on phones
- `layout-sw600dp-land/` folder - Layouts for landscape tablets

In the tablet layouts, I increased the text sizes (28sp → 40sp), padding (24dp → 48dp), and margins to take advantage of the larger screen space. This way, the same app code works perfectly on phones, 7-inch tablets, and 10-inch tablets without any Java code changes. The system automatically selects the correct layout based on the device's screen size and orientation.

## 3. What challenges did you face when combining Bottom Navigation and Tabs?

**Challenge 1: Navigation Hierarchy Conflict**
The bottom navigation represents top-level destinations (Home, Profile, Settings), while the tabs inside Profile represent secondary navigation (Info, Gallery). I solved this by keeping the TabLayout and ViewPager2 only inside ProfileFragment instead of making them part of the main navigation graph. This prevents conflicts between the two navigation systems.

**Challenge 2: Back Stack Management**
The BottomNavigationView replaces fragments on each click, while TabLayout switches between fragments within the same destination. I ensured each bottom navigation item maintains its own independent back stack, so navigating back from Settings goes to the last visited state in that section.

**Challenge 3: State Preservation**
When switching between bottom navigation items, the tab selection in ProfileFragment could be lost. I solved this by saving the ViewPager position in the fragment and restoring it in `onViewCreated()`. This ensures users see the same tab they were on when they return to Profile.
