# Cline Rule: No Cruft Code Policy

rules:
  no_cruft_code:
    description: "Prevent creation of prefixed/suffixed files that leave legacy code behind"

    prohibited_actions:
      - "Creating files with prefixes like 'Enhanced', 'Improved', 'Fixed', 'New', 'Updated', 'Better'"
      - "Creating files with suffixes like 'V2', 'V3', 'New', 'Updated', 'Fixed'"
      - "Keeping old files when creating replacements"
      - "Commenting out large blocks of code instead of removing them"

    required_actions:
      - "ALWAYS replace existing files in-place when making improvements"
      - "ALWAYS remove old files when creating replacements"
      - "Use version control (git) for history, not file naming"
      - "If major refactoring is needed, create feature branch but still replace files"

    enforcement:
      - "Before creating any new file, check if it's replacing an existing one"
      - "If replacing functionality, DELETE the old file in the same commit"
      - "If uncertain about replacement, ASK before creating new files"
      - "Use descriptive commit messages to explain what was replaced"

    examples:
      BAD:
        - "TrackerFetcher.js" + "EnhancedTrackerFetcher.js" (both exist)
        - "UserService.js" + "UserServiceV2.js" (both exist)
        - "// OLD CODE - keeping for reference" (commented blocks)

      GOOD:
        - Replace TrackerFetcher.js content directly
        - Use git history to see previous versions
        - Clean removals with clear commit messages

    exceptions:
      - "Temporary files during development (must be cleaned up before PR)"
      - "A/B testing scenarios (with clear removal timeline)"
      - "Gradual migration with documented timeline and cleanup plan"

# Integration with Cline
prompt_additions:
  - "When modifying existing functionality, REPLACE files in-place rather than creating new ones"
  - "If you're about to create a file with Enhanced/Improved/Fixed/New prefix, STOP and ask if you should replace the existing file instead"
  - "Always confirm file replacements and deletions with the user"
  - "Remind user to remove old files if any are discovered during development"
