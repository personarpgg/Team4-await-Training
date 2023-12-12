1. 딜레이 시간 관련하여
introduceTeam프로젝트를 진행하며 setTimeout과 setInterval을 이용한 호출 스케줄링 관리를 사용 중
await메소드를 지향하고자 예시파일 작성과 간단한 분석을 작성하였습니다.

2. 해당 코드에선 2초후 발생하는 함수(resolveAfter2Seconds)를 통해
생성자 함수(new Promise())로 반환하게 되는데
그 과정에서 x의 값(console.log(x))을 setTimeout의 딜레이 과정[원형]과
setTimeout와 setInterval을 사용하지 않고[변형] await를 이용해 딜레이를 구현할 수 있는 방법을 테스트하는 코드입니다.


[원형]
function resolveAfter2Seconds(x) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}

async function f1() {
  var x = await resolveAfter2Seconds(10);
  console.log(x); // 10
}

f1();

[변형]
// 주어진 밀리초(ms) 동안 대기하는 함수
const delay = (ms) => new Promise(resolve => setTimeout(resolve, ms));

// 비동기 함수
async function f1() {
  console.log('Start');

  // 2초 동안 대기
  await delay(2000);

  console.log('After 2 seconds');
}

// 비동기 함수 호출
f1();
