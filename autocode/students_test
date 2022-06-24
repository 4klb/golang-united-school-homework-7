package coverage

import (
	"errors"
	"os"
	"testing"
	"time"

	"github.com/stretchr/testify/assert"
)

var (
	errGotWant  = "got %v want %v"
	errSetValue = "could not put a value into the matrix"
	errNew      = "could not create a matrix"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func Test_Len(t *testing.T) {
	sdata := []struct {
		people   People
		Expected int
	}{
		{
			people: People{
				{
					firstName: "J.R.R.",
					lastName:  "Tolkien",
					birthDay:  time.Now(),
				},
				{
					firstName: "Sergey",
					lastName:  "Brin",
					birthDay:  time.Now(),
				},
				{
					firstName: "Sergey",
					lastName:  "Brin",
					birthDay:  time.Now(),
				},
			},
			Expected: 3,
		},
	}
	for _, data := range sdata {
		got := data.people.Len()
		if !assert.Equal(t, got, data.Expected) {
			t.Errorf(errGotWant, got, data.Expected)
		}
	}
}

func Test_Less(t *testing.T) {
	data := []struct {
		people   People
		Expected []bool
	}{
		{
			people: People{
				{
					firstName: "J.R.R.",
					lastName:  "Tolkien",
					birthDay:  time.Now(),
				},
				{
					firstName: "J.R.R.",
					lastName:  "Obama",
					birthDay:  time.Now(),
				},
				{
					firstName: "Sergey",
					lastName:  "Brin",
					birthDay:  time.Now(),
				},
				{
					firstName: "J.R.R.",
					lastName:  "Brin",
					birthDay:  time.Now().Add(20 * time.Second),
				},
			},
			Expected: []bool{false, true, false, false},
		},
	}
	for _, tcase := range data {
		for i := 0; i < len(tcase.people)-1; i++ {
			got := tcase.people.Less(i, i+1)
			if !assert.Equal(t, got, tcase.Expected[i]) {
				t.Errorf(errGotWant, got, tcase.Expected[i])
			}
		}
	}
}

func Test_Swap(t *testing.T) {
	data := []struct {
		people People
	}{
		{
			people: People{
				{
					firstName: "J.R.R.",
					lastName:  "Tolkien",
					birthDay:  time.Now(),
				},
				{
					firstName: "Agey",
					lastName:  "Arin",
					birthDay:  time.Now(),
				},
			},
		},
		{
			people: People{
				{
					firstName: "J.R.R.",
					lastName:  "Tolkien",
					birthDay:  time.Now(),
				},
				{
					firstName: "Agey",
					lastName:  "Arin",
					birthDay:  time.Now(),
				},
			},
		},
	}

	for i := 0; i < len(data)-1; i++ {
		f := data[i].people[i]
		s := data[i].people[i+1]
		data[i].people.Swap(i, i+1)
		if !assert.Equal(t, f, data[i].people[i+1]) &&
			!assert.Equal(t, s, data[i].people[i]) {
			t.Errorf("got %v %v want %v %v", i, i+1, s, f)
		} else {
			continue
		}
	}
}

func Test_New(t *testing.T) {
	data := map[string]struct {
		arg string
		err error
	}{
		"correct": {
			arg: `15 54 44
			12 12 43
			23 52 32`,
		},
		"syntax error": {
			arg: `15t 54 44
			12 12 43
			23 52 32`,
			err: errors.New("invalid syntax"),
		},
		"not equal rows": {
			arg: `15 54 44 99
			12 12 43
			23 52 32`,
			err: errors.New("Rows need to be the same length"),
		},
	}

	for _, value := range data {
		_, err := New(value.arg)
		if err != nil && value.err == err {
			t.Errorf(errNew)
			return
		}
	}
}

func Test_Rows(t *testing.T) {
	var j, k int

	data := struct {
		matrix   Matrix
		Expected [][]int
	}{
		matrix: Matrix{
			rows: 3,
			cols: 4,
			data: []int{
				15, 54, 44, 42,
				12, 12, 43, 516,
				23, 52, 32, 36,
			},
		},
		Expected: [][]int{
			{15, 54, 44, 42},
			{12, 12, 43, 516},
			{23, 52, 32, 36},
		},
	}

	got := data.matrix.Rows()

	for i := 0; i < len(data.Expected) && j < len(got); i++ {
		if !assert.Equal(t, data.Expected[k], got[k]) {
			t.Errorf(errGotWant, got[k], data.Expected[k])
		}
		j++
		k++
	}
}

func Test_Cols(t *testing.T) {
	var j, k int

	data := struct {
		matrix   Matrix
		Expected [][]int
	}{
		matrix: Matrix{
			rows: 3,
			cols: 4,
			data: []int{
				15, 54, 44, 42,
				12, 12, 43, 516,
				23, 52, 32, 36,
			},
		},
		Expected: [][]int{
			{15, 12, 23},
			{54, 12, 52},
			{44, 43, 32},
			{42, 516, 36},
		},
	}

	got := data.matrix.Cols()

	for i := 0; i < len(data.Expected) && j < len(got); i++ {
		if !assert.Equal(t, data.Expected[k], got[k]) {
			t.Errorf(errGotWant, got[k], data.Expected[k])
		}
		j++
		k++
	}
}

func Test_Set(t *testing.T) {
	data := map[string]struct {
		matrix   Matrix
		Expected bool
		rows     int
		cols     int
		value    int
	}{
		"correct": {
			matrix: Matrix{
				rows: 3,
				cols: 3,
				data: []int{
					15, 54, 44,
					12, 12, 43,
					23, 52, 32,
				},
			},
			Expected: true,
			rows:     0,
			cols:     0,
			value:    99,
		},
		"rows<0": {
			matrix: Matrix{
				rows: -1,
				cols: 3,
				data: []int{
					15, 54, 44,
					12, 12, 43,
					23, 52, 32,
				},
			},
			Expected: false,
			rows:     5,
			cols:     0,
			value:    99,
		},
		"cols<0": {
			matrix: Matrix{
				rows: 3,
				cols: -1,
				data: []int{
					15, 54, 44,
					12, 12, 43,
					23, 52, 32,
				},
			},
			Expected: false,
			rows:     0,
			cols:     5,
			value:    99,
		},
		"rows=": {
			matrix: Matrix{
				rows: 3,
				cols: 3,
				data: []int{
					15, 54, 44,
					12, 12, 43,
					23, 52, 32,
				},
			},
			Expected: false,
			rows:     3,
			cols:     0,
			value:    99,
		},
		"cols=": {
			matrix: Matrix{
				rows: 3,
				cols: 3,
				data: []int{
					15, 54, 44,
					12, 12, 43,
					23, 52, 32,
				},
			},
			Expected: false,
			rows:     0,
			cols:     3,
			value:    99,
		},
	}

	for _, tcase := range data {
		got := tcase.matrix.Set(tcase.rows, tcase.cols, tcase.value)
		if !assert.Equal(t, got, tcase.Expected) {
			t.Errorf(errSetValue)
		}
	}
}
