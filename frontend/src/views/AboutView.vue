<template>
  <div class="about">
    <h1>off_the_record</h1>
    <p class="subtitle">
      Windows C++ 에이전트가 키 입력 이벤트 기반으로 타이핑 메트릭(keystroke count 등)을 집계하고,
      Spring Boot 백엔드로 전송해 실시간 처리 및 저장/스트리밍하는 이벤트 파이프라인 토이 프로젝트입니다.
    </p>

    <section>
      <h2>System Overview</h2>
      <ul>
        <li>
          <b>Windows Agent (C++/WinAPI)</b>:
          키 입력 기반 메트릭 집계(keystroke count 등) → JSON 직렬화
        </li>
        <li><b>WebSocket</b>: Agent → Backend 실시간 전송(양방향 채널)</li>
        <li><b>Spring Boot (Java 17)</b>: 세션/커넥션 관리, 메트릭 처리 및 영속화</li>
        <li><b>MySQL + Flyway</b>: 메트릭 데이터 영속 저장, 스키마 버전 관리</li>
        <li><b>SSE</b>: Backend → Frontend 실시간 푸시 스트리밍</li>
        <li><b>REST API</b>: Frontend → Backend 제어(수집 시작/중지 등)</li>
      </ul>

      <div class="flow">
        <code>
          Agent(C++) → WebSocket(JSON) → Spring Boot → MySQL(Flyway) → SSE → Vue UI
        </code>
      </div>
    </section>

    <section>
      <h2>Core Capabilities</h2>
      <ul>
        <li>에이전트 등록 및 세션/커넥션 관리 (machineGuid 기반 식별)</li>
        <li>실시간 메트릭 업데이트 및 스트리밍 (WebSocket + SSE)</li>
        <li>메트릭 저장 및 조회 (MySQL, 마이그레이션/버전 관리: Flyway)</li>
        <li>수집 제어 엔드포인트 제공 (Start/Stop)</li>
      </ul>
    </section>

    <section>
      <h2>Motivation</h2>
      <p>
        단순 CRUD를 넘어, 입력 이벤트 기반 메트릭 집계부터 네트워크 전송, 서버 아키텍처, 데이터 영속화까지
        end-to-end로 설계/구현 경험을 쌓고, 동시성 및 실시간 통신 설계를 포트폴리오로 보여주기 위해 만들었습니다.
      </p>
    </section>

    <section class="notice">
      <h2>Ethics & Safety</h2>
      <ul>
        <li>본 프로젝트는 <b>학습/검증 목적</b>이며, 사용자 <b>명시적 동의</b> 하에서만 사용해야 합니다.</li>
        <li>
          민감정보(비밀번호/개인정보 등)는 수집/전송/저장되지 않도록
          <b>필터링 및 마스킹</b>이 필요합니다.
        </li>
        <li>
          원문 키 입력(문자열) 저장이 아닌 <b>집계 메트릭</b> 중심으로 설계하여
          프라이버시 리스크를 최소화합니다.
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  mounted() {
    console.log("[AboutView] mounted.");
  },
};
</script>

<style scoped>
.about { max-width: 900px; margin: 0 auto; padding: 24px; }
.subtitle { margin-top: 8px; color: #666; }
section { margin-top: 24px; }
.flow { margin-top: 8px; padding: 12px; background: #f6f6f6; border-radius: 8px; }
.notice { border-left: 4px solid #ff6b6b; padding-left: 12px; }
</style>
