735. Asteroid Collision
We are given an array asteroids of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

Example 1:

Input: asteroids = [5,10,-5] Output: [5,10] Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide. Example 2:

Input: asteroids = [8,-8] Output: [] Explanation: The 8 and -8 collide exploding each other. Example 3:

Input: asteroids = [10,2,-5] Output: [10] Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.


Attempt 2: 01/08 -> 257/275 TestCases
Code 
```
function checkPositiveAndNegativeCombition(num1: number, num2: number) {
    if (num1 == null || num2 == null) {
        return false;
    }
    if ((num1 > 0 && num2 < 0) ) {
        return true;
    }
    return false;
}

function asteroidsCollidedResult(numStack: number[], asteroid: number) {
    let n = numStack.length;
    console.log(numStack)
    if (checkPositiveAndNegativeCombition(numStack[n - 1], asteroid) && numStack[n-1] + asteroid === 0) {
        numStack.pop();
    }
    else {
        numStack.push(asteroid);
        while (checkPositiveAndNegativeCombition(numStack[n - 1], numStack[n])) {
            const x = numStack.pop();
            const y = numStack.pop();
            console.log(Math.abs(x) > Math.abs(y) ? x : y);
            numStack.push(Math.abs(x) > Math.abs(y) ? x : y)
            n = numStack.length - 1;
        }
    }

}

function asteroidCollision(asteroids: number[]): number[] {
    const numStack = [];
    if (asteroids.length === 0) {
        return [];
    }
    numStack.push(asteroids[0]);
    for (let i = 1; i < asteroids.length; i++) {
        asteroidsCollidedResult(numStack, asteroids[i]);
    }
    return numStack;
};
```
