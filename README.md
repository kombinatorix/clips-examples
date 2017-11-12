# clips-examples #
Collection of examples of CLIPS code. Maybe you find the answer to your CLIPS related question.

## Manipulate integers and floats ##

```CLIPS
(deffunction inc-by-one (?var)
    (bind ?var (+ ?var 1))
    (return ?var)
)
```

```
CLIPS> (inc-by-one 1)
2
CLIPS> (inc-by-one 1.1)
2.1
CLIPS> (inc-by-one -3)
-2
```

```CLIPS
(deffunction add-x-to-y (?y ?x)
    (bind ?y (+ ?y ?x))
    (return ?y)
)
```

```
CLIPS> (add-x-to-y 1 -3.5)
-2.5
```

```CLIPS

(deffunction add-one-to-list-of-numbers (?lon)
    (progn$ (?field ?lon)
        (bind ?lon (replace$ ?lon ?field-index ?field-index (+ ?field 1)))
    )
    (return ?lon)
)

```

```CLIPS

(deffunction add-one-to-list-of-numbers-alt (?lon)
    (loop-for-count (?cnt (length ?lon))
        (bind ?lon (replace$ ?lon ?cnt ?cnt (+(nth$ ?cnt ?lon) 1)))
    )
    (return ?lon) 
)

```


```
CLIPS> (bind ?numbers (create$ 4 3 5 1 8))
(4 3 5 1 8)
CLIPS> (add-one-to-list-of-numbers ?numbers)
(5 4 6 2 9)
CLIPS> (add-one-to-list-of-numbers-alt ?numbers)
(5 4 6 2 9)
```


```CLIPS
(deffunction add-one-list-to-another (?list-one ?list-two)
    (progn$ (?field ?list-one)
        (bind ?list-one (replace$ ?list-one ?field-index ?field-index 
            (+ ?field (nth$ ?field-index ?list-two)))
    	)
    )
    (return ?list-one)
)
```

```
CLIPS> (bind ?list-one (create$ 1 1 1 -1 -1 -1 1.0 1.0 1.0))
(1 1 1 -1 -1 -1 1.0 1.0 1.0)
CLIPS> (bind ?list-two (create$ 1 -1 1.0 1 -1 1.0 1 -1 1.0))
(1 -1 1.0 1 -1 1.0 1 -1 1.0)
CLIPS> (add-one-list-to-another ?list-one ?list-two)
(2 0 2.0 0 -2 0.0 2.0 0.0 2.0)
```


