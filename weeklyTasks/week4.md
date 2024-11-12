### **3.1: Collect User Preferences**
   - **Objective**: Gather user-specific information to guide recipe generation and personalize recommendations.
   - **Sub-Steps**:
     - **3.1.1: Preference Input Interface**:
       - Design a user-friendly interface (e.g., a form or survey) for users to specify their preferences.
       - Include options for dietary restrictions (e.g., vegetarian, vegan, gluten-free), preferred cuisines, cooking difficulty, and nutritional goals (e.g., low-carb, high-protein).
     - **3.1.2: Store User Preferences**:
       - Store these preferences in a structured format (e.g., a JSON file, SQL database).
       - Ensure each preference can be quickly retrieved and mapped to the appropriate states in the Markov Chain.
     - **3.1.3: Update Preferences Dynamically**:
       - Allow users to update preferences and adjust the matrix accordingly in real-time or for future sessions.

---

### **3.2: Filter States Based on Preferences**
   - **Objective**: Adjust the Markov Chain’s state space to match user preferences.
   - **Sub-Steps**:
     - **3.2.1: Tag States for Dietary and Cuisine Filters**:
       - Label each ingredient and step state with dietary tags (e.g., “vegetarian”, “gluten-free”) and cuisine type.
     - **3.2.2: Create Filtered State Lists**:
       - Generate a filtered list of states that match the user’s dietary and cuisine preferences. For example, if the user is vegetarian, exclude all meat-based ingredients from the available state list.
     - **3.2.3: Update Transition Matrix Based on Filtered States**:
       - Use the filtered list to modify the transition matrix, setting transition probabilities to zero for any transitions involving excluded states.
     - **3.2.4: Validate Adjustments**:
       - Ensure the adjusted matrix still functions as a valid Markov Chain, where each row’s probabilities sum to 1.

---

### **3.3: Personalize Transition Probabilities Based on User History**
   - **Objective**: Adapt the transition probabilities based on the user’s previous interactions to prioritize frequently used ingredients or steps.
   - **Sub-Steps**:
     - **3.3.1: Track User Interaction History**:
       - Record user interactions with generated recipes, noting preferred ingredients, cooking steps, and cuisines.
       - Calculate a frequency count for each ingredient and step used in past recipes.
     - **3.3.2: Create a Personalized Transition Matrix**:
       - Adjust the base transition matrix by increasing probabilities for transitions involving frequently used ingredients or steps.
       - For example, if the user frequently selects “tomato” in Italian recipes, increase the transition probability for “tomato” to follow other Italian ingredients.
     - **3.3.3: Apply Weighting Mechanisms**:
       - Apply a weighting factor to the transition probabilities based on user history. For instance, a commonly chosen ingredient might receive a weight of 1.2, whereas less-used ingredients receive a weight of 0.8.
     - **3.3.4: Normalize Transition Matrix**:
       - After weighting, re-normalize each row to ensure the probabilities sum to 1.
     - **3.3.5: Test for Consistency**:
       - Run test scenarios to confirm that the personalized transition matrix produces recipes aligned with the user’s known preferences.

---

### **3.4: Incorporate Ingredient Availability**
   - **Objective**: Adjust the Markov Chain to consider only the ingredients the user currently has at home, guiding recipe generation based on available resources.
   - **Sub-Steps**:
     - **3.4.1: Interface for Ingredient Availability Input**:
       - Create a feature in the interface where users can specify available ingredients (e.g., by scanning, typing, or uploading a list).
     - **3.4.2: Filter Transition Matrix Based on Available Ingredients**:
       - Cross-reference available ingredients with the list of states in the transition matrix.
       - Set transition probabilities to zero for any transitions involving unavailable ingredients.
     - **3.4.3: Adjust Matrix with Zeroed Transitions**:
       - Re-calculate the transition matrix where each row only includes transitions to available ingredients.
       - Re-normalize each row so that the probabilities still sum to 1 after removing unavailable options.
     - **3.4.4: Real-Time Updates for Ingredient Changes**:
       - Allow users to add or remove ingredients in real-time, adjusting the matrix dynamically to reflect these changes.

---

### **3.5: Create Composite Personalized Matrix**
   - **Objective**: Combine all preference adjustments into a single transition matrix tailored to the user’s preferences and ingredient availability.
   - **Sub-Steps**:
     - **3.5.1: Merge Dietary and Cuisine Adjustments**:
       - Combine the filtered matrix from user dietary and cuisine preferences with the weighted probabilities from user history.
     - **3.5.2: Integrate Ingredient Availability Matrix**:
       - Apply the ingredient availability adjustments on top of the preference and history adjustments to ensure only accessible ingredients are used.
     - **3.5.3: Finalize and Validate the Composite Matrix**:
       - Perform a final check to ensure each row sums to 1 and that all states align with the user’s preferences and available ingredients.
       - Test with sample recipes to verify the model produces personalized outputs that meet the user’s preferences.

---

### **3.6: Testing and Feedback Mechanism for Personalization**
   - **Objective**: Test the effectiveness of the personalization logic and gather user feedback.
   - **Sub-Steps**:
     - **3.6.1: Conduct Initial User Testing**:
       - Run test cases where users generate recipes to confirm the personalization logic works as expected.
     - **3.6.2: Collect Feedback on Personalization**:
       - Ask users to rate recipe relevance and alignment with their preferences.
       - Use feedback to adjust weighting factors or transition probabilities for better personalization.
     - **3.6.3: Implement Adaptive Learning**:
       - Allow the model to update user history and ingredient preferences over time, adapting transition probabilities as user interactions increase.
