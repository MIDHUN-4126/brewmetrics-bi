# Reflection

Working on the BrewMetrics project with GitHub Copilot
changed the way I approached Power BI development compared
with a normal single-file laboratory exercise. Copilot was
particularly useful when creating initial DAX structures
for time-based calculations, running totals, and rankings.
However, I still had to validate the generated expressions
against the actual semantic model and modify calculations
when the generated logic did not completely match the
required analysis.

One important lesson was that AI-generated DAX should not
be accepted without testing. I checked the measures using
Power BI visuals and verified whether the results changed
correctly when filters and dimensions were applied. This
also helped me understand the difference between generating
a syntactically valid expression and creating a measure that
actually answers the business question.

Using Git also changed my workflow. Instead of building the
entire Power BI solution and saving one final file, I created
separate commits for the star schema, individual DAX
measures, dashboard, and documentation. This made the
development process traceable and allowed each stage to be
reviewed independently. The commit history therefore became
part of the project deliverable rather than just a backup.