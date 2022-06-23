package coverage

import (
	"log"
	"os"
	"testing"
	"time"
)

var (
	errGotWant = "got %v want %v"
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
		if got != data.Expected {
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
			if got != tcase.Expected[i] {
				t.Errorf("got %v want %v", got, tcase.Expected[i])
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
		if f != data[i].people[i+1] && s != data[i].people[i] {
			t.Errorf("got %v %v want %v %v", i, i+1, s, f)
		} else {
			continue
		}
	}
}

func Test_New(t *testing.T) {
	data := []struct {
		matrix   Matrix
		Expected [][]int
	}{
		{
			matrix: Matrix{
				rows: 3,
				cols: 4,
				data: []int{
					15, 54, 44, 42,
					12, 12, 43, 516,
					23, 52, 32, 36,
				},
			},
		},
	}

	for _, data := range data {
		var j int
		got, err := New(`15, 54, 44, 42,
		12, 12, 43, 516,
		23, 52, 32, 36,
		`)
		if err != nil {
			log.Println(err)
			return
		}

		if got.rows != data.matrix.rows {
			t.Errorf(errGotWant, got.rows, data.matrix.rows)
		} else if got.cols != data.matrix.cols {
			t.Errorf(errGotWant, got.cols, data.matrix.cols)
		}
		for i := 0; i < len(got.data) && j < len(data.matrix.data); i++ {
			if got.data[i] != data.matrix.data[j] {
				t.Errorf(errGotWant, got.data[i], data.matrix.data[j])
			}
			j++
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
		res := Compare(data.Expected[k], got[k])
		if !res {
			t.Errorf(errGotWant, got[k], data.Expected[k])
		}
		j++
		k++
	}
}

func Compare(arr1, arr2 []int) bool {
	var j int
	for i := 0; i < len(arr1)-1 && j < len(arr2)-1; i++ {
		if arr1[i] != arr2[j] {
			return false
		}
		j++
	}
	return true
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
		res := Compare(data.Expected[k], got[k])
		if !res {
			t.Errorf(errGotWant, got[k], data.Expected[k])
		}
		j++
		k++
	}
}

func Test_Set(t *testing.T) {
	var j, k int

	data := []struct {
		matrix   Matrix
		Expected [][]int
		rows     int
		cols     int
		value    int
	}{
		{
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
				{99, 54, 44, 42},
				{12, 12, 43, 516},
				{23, 52, 32, 36},
			},
			rows:  -1,
			cols:  0,
			value: 99,
		},
		{
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
				{99, 54, 44, 42},
				{12, 12, 43, 516},
				{23, 52, 32, 36},
			},
			rows:  0,
			cols:  0,
			value: 99,
		},
	}

	for _, d := range data {
		got := d.matrix.Set(d.rows, d.cols, d.value)
		// got := data.matrix[i].Set(i)

		if !got {
			t.Errorf("could not put a value into the matrix")
		}

		// got = data.matrix.Set(0, 0, 99)

		getRows := d.matrix.Rows()

		for i := 0; i < len(d.Expected) && j < len(getRows); i++ {
			res := Compare(d.Expected[k], getRows[k])
			if !res {
				t.Errorf(errGotWant, getRows[k], d.Expected[k])
			}
			j++
			k++
		}
	}
}
