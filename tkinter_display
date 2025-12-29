import tkinter as tk
from tkinter import ttk
from solver import solve_all

# ------------------ UNIT CONFIG ------------------
UNIT_SYSTEMS = {
    "SI": {
        "u": 1,
        "v": 1,
        "a": 1,
        "s": 1,
        "t": 1
    },
    "CGS": {
        "u": 100,
        "v": 100,
        "a": 100,
        "s": 100,
        "t": 1
    }
}

UNIT_LABELS = {
    "SI": {
        "u": "m/s",
        "v": "m/s",
        "a": "m/s²",
        "s": "m",
        "t": "s"
    },
    "CGS": {
        "u": "cm/s",
        "v": "cm/s",
        "a": "cm/s²",
        "s": "cm",
        "t": "s"
    }
}

# ------------------ ROOT ------------------
root = tk.Tk()
root.title("Kinematics Solver")
root.geometry("900x800")
root.configure(bg="#020617")
root.resizable(False, False)

# ------------------ STYLES ------------------
style = ttk.Style()
style.theme_use("clam")

# ------------------ VARIABLES ------------------
unit_var = tk.StringVar(value="SI")

# ------------------ HELPERS ------------------
def get_value(entry):
    try:
        return float(entry.get().strip())
    except:
        return None

# ------------------ ANIMATION ------------------
def animate_text(lines, index=0):
    if index >= len(lines):
        output_text.config(state="disabled")
        return
    output_text.insert("end", lines[index][0], lines[index][1])
    output_text.after(90, animate_text, lines, index + 1)

# ------------------ CALCULATE ------------------
def calculate():
    unit = unit_var.get()
    factors = UNIT_SYSTEMS[unit]

    values = {}
    for var, entry in entries.items():
        val = get_value(entry)
        values[var] = val / factors[var] if val is not None else None

    results_si = solve_all(values)

    output_text.config(state="normal")
    output_text.delete("1.0", "end")

    animated_lines = []
    units = UNIT_LABELS[unit]

    animated_lines.append(("Results\n\n", "title"))

    for var in ["u", "v", "a", "s", "t"]:
        if results_si.get(var) is not None:
            display_val = results_si[var] * factors[var]
            animated_lines.append((f"{var} = ", "given"))
            animated_lines.append(
                (f"{display_val:.4f} {units[var]}\n", "calculated")
            )

    animate_text(animated_lines)

# ------------------ CONTAINER ------------------
container = tk.Frame(root, bg="#020617")
container.pack(fill="both", expand=True, padx=30, pady=25)

# ------------------ TITLE ------------------
tk.Label(
    container,
    text="Kinematics Solver",
    font=("Segoe UI", 26, "bold"),
    fg="#38bdf8",
    bg="#020617"
).pack(pady=(0, 25))

# ------------------ UNIT SELECT ------------------
unit_frame = tk.Frame(container, bg="#020617")
unit_frame.pack(pady=(0, 20))

tk.Label(
    unit_frame,
    text="Unit System:",
    font=("Segoe UI", 13),
    fg="#e5e7eb",
    bg="#020617"
).pack(side="left", padx=10)

ttk.Combobox(
    unit_frame,
    textvariable=unit_var,
    values=["SI", "CGS"],
    state="readonly",
    width=10
).pack(side="left")

# ------------------ INPUT CARD ------------------
input_card = tk.Frame(container, bg="#020617", highlightbackground="#1e293b", highlightthickness=2)
input_card.pack(fill="x", pady=(0, 20))

tk.Label(
    input_card,
    text="Known Values",
    font=("Segoe UI", 16, "bold"),
    fg="#e5e7eb",
    bg="#020617"
).pack(anchor="w", padx=15, pady=(10, 5))

input_grid = tk.Frame(input_card, bg="#020617")
input_grid.pack(padx=20, pady=10)

labels = {
    "u": "Initial Velocity (u)",
    "v": "Final Velocity (v)",
    "a": "Acceleration (a)",
    "t": "Time (t)",
    "s": "Displacement (s)"
}

entries = {}

for i, (var, text) in enumerate(labels.items()):
    tk.Label(
        input_grid,
        text=text,
        font=("Segoe UI", 12),
        fg="#cbd5f5",
        bg="#020617"
    ).grid(row=i, column=0, sticky="w", pady=8)

    entry = tk.Entry(
        input_grid,
        font=("Segoe UI", 12),
        width=18,
        bg="#020617",
        fg="#e5e7eb",
        insertbackground="white",
        highlightthickness=1,
        highlightbackground="#334155",
        highlightcolor="#38bdf8"
    )
    entry.grid(row=i, column=1, padx=15, pady=8)
    entries[var] = entry

# ------------------ BUTTON ------------------
tk.Button(
    container,
    text="CALCULATE",
    font=("Segoe UI", 14, "bold"),
    bg="#38bdf8",
    fg="#020617",
    activebackground="#0ea5e9",
    activeforeground="white",
    bd=0,
    padx=35,
    pady=12,
    command=calculate
).pack(pady=15)

# ------------------ OUTPUT CARD ------------------
output_card = tk.Frame(container, bg="#020617", highlightbackground="#1e293b", highlightthickness=2)
output_card.pack(fill="both", expand=True)

tk.Label(
    output_card,
    text="Results",
    font=("Segoe UI", 16, "bold"),
    fg="#e5e7eb",
    bg="#020617"
).pack(anchor="w", padx=15, pady=(10, 5))

output_text = tk.Text(
    output_card,
    font=("Consolas", 14),
    bg="#020617",
    fg="#e5e7eb",
    padx=20,
    pady=15,
    wrap="word",
    height=8,
    bd=0
)
output_text.pack(fill="both", expand=True, padx=15, pady=10)

# ------------------ TEXT STYLES ------------------
output_text.tag_configure("title", foreground="#38bdf8", font=("Consolas", 15, "bold"))
output_text.tag_configure("given", foreground="#94a3b8")
output_text.tag_configure("calculated", foreground="#22c55e", font=("Consolas", 14, "bold"))

output_text.config(state="disabled")

# ------------------ MAIN LOOP ------------------
root.mainloop()


