def eq1(values):
    u, v, a, t = values["u"], values["v"], values["a"], values["t"]

    known = [u, v, a, t].count(None)
    if known != 1:
        return None

    if v is None:
        return "v", u + a * t
    if u is None:
        return "u", v - a * t
    if a is None:
        return "a", (v - u) / t
    if t is None:
        return "t", (v - u) / a



def eq2(values):
    u, s, a, t = values["u"], values["s"], values["a"], values["t"]

    known = [u, s, a, t].count(None)
    if known != 1:
        return None

    if s is None:
        return "s", u * t + 0.5 * a * t * t
    if u is None:
        return "u", (s - 0.5 * a * t * t) / t
    if a is None:
        return "a", 2 * (s - u * t) / (t * t)
    if t is None:
        # quadratic → skip for now
        return None



def eq3(values):
    u, v, a, s = values["u"], values["v"], values["a"], values["s"]

    known = [u, v, a, s].count(None)
    if known != 1:
        return None

    if v is None:
        return "v", (u * u + 2 * a * s) ** 0.5
    if u is None:
        return "u", (v * v - 2 * a * s) ** 0.5
    if a is None:
        return "a", (v * v - u * u) / (2 * s)
    if s is None:
        return "s", (v * v - u * u) / (2 * a)



EQUATIONS = [eq1, eq2, eq3]

def solve_all(values):
    while True:
        progress = False

        for eq in EQUATIONS:
            result = eq(values)
            if result:                         #if any result is there
                var, value = result            #the result is variable and its value 

                if values[var] is None:        #only updates the value if that value was unknown
                    values[var] = value        # updates the value
                    progress = True            #progress is being made

        if not progress:
            break

    return values



if __name__ == "__main__":
    test_values = {
        "u": None,
        "v": 30,
        "a": 4,
        "t": 5,
        "s": None
    }

    print(solve_all(test_values))

