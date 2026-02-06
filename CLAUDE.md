# RNN vs Transformer Assignment - Context for Claude

## Project Overview
This is a Deep Neural Networks Assignment 3 for implementing and comparing RNN (GRU) vs Transformer models for time series forecasting.

**CRITICAL**: Before starting any work, ALWAYS read the `IMPLEMENTATION_PLAN.md` file in this directory for complete context.

## Key Files
- `2025AA05686_rnn_assignment.ipynb` - Main assignment notebook (template with TODOs)
- `IMPLEMENTATION_PLAN.md` - **READ THIS FIRST** - Implementation tracker with decisions, progress, and grading criteria
- `autograder.txt` - Grading algorithm (20 marks breakdown)
- `instructions.pdf` - Original assignment instructions

## Assignment Configuration (FROM IMPLEMENTATION_PLAN.md)
- **Student**: PRITISH JOSHI (2025AA05686)
- **Dataset**: Apple Stock Prices (AAPL) from Yahoo Finance
- **Framework**: Keras/TensorFlow
- **RNN Type**: GRU (not LSTM)
- **Sequence Length**: 30 days lookback
- **Prediction Horizon**: 1 day ahead
- **Train/Test Split**: 90/10 temporal (NO shuffling)

## Mandatory Requirements (Auto-fail if missing)
1. ✅ Positional encoding in Transformer (sin/cos implementation)
2. ✅ Multi-head attention with n_heads > 1
3. ✅ Stacked GRU layers (minimum 2)
4. ✅ All 4 metrics calculated: MAE, RMSE, MAPE, R²
5. ✅ Temporal split only (NO shuffle=True)
6. ✅ Loss tracking: initial_loss and final_loss
7. ✅ JSON output with all required fields
8. ✅ Notebook executed with all outputs visible

## Grading Breakdown (20 marks total)
- GRU Implementation: 5 marks
- Transformer Implementation: 5 marks
- Loss Convergence: 4 marks (need ≥50% reduction for full marks)
- Metrics Calculation: 2 marks
- Analysis Quality: 2 marks (need 8+ key topics)
- Code Structure: 2 marks

## Template Change Policy
**IMPORTANT**: Document ALL changes to the template notebook in `IMPLEMENTATION_PLAN.md` under "Change Log" section.

Only modify TODO sections - do not change:
- Cell structure
- Markdown headers
- Required output formats
- JSON structure

## Work Strategy & Update Protocol

### Core Workflow
1. **Always read IMPLEMENTATION_PLAN.md first** to understand context
2. **PROACTIVELY UPDATE IMPLEMENTATION_PLAN.md** as you work (details below)
3. **Work cell-by-cell and WAIT for user review**: After each cell modification, STOP and wait for user to review, ask questions, and approve before proceeding to next cell
4. Work phase by phase (1→2→3→4→5→6)
5. Test each model independently before comparison
6. Track all variables needed for JSON output
7. Run "Restart & Run All" before submission
8. Verify final checklist in IMPLEMENTATION_PLAN.md

### Interactive Cell-by-Cell Protocol
**CRITICAL**: After modifying ANY cell:
1. ✅ Explain what was changed and why
2. ✅ WAIT for user to review the code
3. ✅ Answer any user questions
4. ✅ Get user approval/feedback before moving to next cell
5. ❌ DO NOT proceed to multiple cells without user confirmation

### Notebook Cell Editing Protocol
**CRITICAL**: When using NotebookEdit tool:
1. ✅ ALWAYS verify the current cell_type before editing (check if it's "code" or "markdown")
2. ✅ If changing cell_type from markdown to code, MUST use the cell_type parameter
3. ✅ After editing, verify the change was applied correctly using Read tool or Bash
4. ✅ Never assume a cell type - always check the actual notebook state
5. ❌ DO NOT batch edit multiple cells without verifying each one individually

### CRITICAL: Autonomous Update Protocol (Applies Across ALL Sessions)

**IMPLEMENTATION_PLAN.md is a LIVING DOCUMENT - update it continuously, NOT at the end.**

**When to Update** (Claude must autonomously decide):
- ✅ After completing any phase or subtask → Update status to "✅ COMPLETED"
- ✅ After making decisions → Document in relevant phase section
- ✅ After modifying template cells → Add to Change Log with cell IDs
- ✅ After filling key variables → Note values (n_samples, loss, metrics)
- ✅ After completing checklist items → Check off boxes
- ✅ When encountering issues → Add to Notes & Observations
- ✅ After discovering important information → Update relevant section

**What to Update**:
- Phase status (⬜ NOT STARTED → 🔄 IN PROGRESS → ✅ COMPLETED)
- Checklist boxes (- [ ] → - [x])
- Change Log with timestamp, cells modified, and values set
- Notes & Observations section with any issues or insights
- Architecture decisions if they differ from plan

**Why This Matters**:
This enables seamless session continuity. Future Claude instances (or you in next session) will know exactly what's been done, what decisions were made, and what's pending.

## Common Pitfalls to Avoid
- ❌ Using shuffle=True anywhere (violates temporal order)
- ❌ Forgetting positional encoding (0 marks for transformer)
- ❌ Single-head attention (loses marks)
- ❌ Missing initial_loss/final_loss tracking
- ❌ Incomplete JSON structure
- ❌ Cleared outputs in notebook
- ❌ Filename mismatch with BITS ID
- ❌ Forgetting to update IMPLEMENTATION_PLAN.md as you work
- ❌ Batch editing multiple cells without checking each one
- ❌ Assuming cell types without verification
- ❌ Not being thorough and careful with each step

## Session Continuity
When resuming work:
1. Read `IMPLEMENTATION_PLAN.md` for full context
2. Check "Change Log" section for what's been modified
3. Review phase statuses to see what's completed
4. Look at current notebook state
5. Continue from last incomplete phase

---

**Remember**:
- IMPLEMENTATION_PLAN.md is the source of truth for all decisions, progress, and requirements
- Update it proactively as you work - it's your project memory across sessions
