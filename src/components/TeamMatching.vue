<template>
    <div>

        <div class="team-container">
            <div class="team" v-for="(team, key) in teamList" :key="key">
                <div class="team-name">
                    {{ team.name }} Team
                </div>
                <div class="user-list">
                    <draggable v-model="team.users" group="user" item-key="number">
                        <template #item="{ element }">
                            <div class="user">{{ element.number }}. {{ element.name }}</div>
                        </template>
                    </draggable>
                </div>

            </div>
        </div>
        <div class="text-center">
            <v-btn color="primary" @click="autoMatch">팀 자동배정</v-btn>
        </div>

        <div class="waiting-container">
            <draggable v-model="waitingList" group="user" item-key="number">
                <template #item="{ element }">
                    <div class="user">{{ element.number }}. {{ element.name }}</div>
                </template>

            </draggable>

        </div>


    </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
    components: {
        draggable,
    },
    data() {
        return {
            teamList: [{
                name: 1,
                users: []
            },
            {
                name: 2,
                users: []
            }, {
                name: 3,
                users: []
            }, {
                name: 4,
                users: []
            }],
            waitingList: [
            ]
        }
    },
    mounted() {


    },
    methods: {
        autoMatch() {
            //팀 자동 매칭

            //1. waitingList의 user를 랜덤으로 뽑아서 teamList에 가장 적은 사용자가 있는 팀에 넣는다.
            //2. waitingList의 user를 teamList에서 제거한다.
            //3. waitingList의 user가 없을 때까지 1,2를 반복한다.
            //4. waitingList의 user가 없으면 종료한다.

            while (this.waitingList.length > 0) {
                let randomIndex = Math.floor(Math.random() * this.waitingList.length);
                let randomUser = this.waitingList[randomIndex];
                let minTeam = this.teamList[0];
                for (let i = 1; i < this.teamList.length; i++) {
                    if (minTeam.users.length > this.teamList[i].users.length) {
                        minTeam = this.teamList[i];
                    }
                }
                minTeam.users.push(randomUser);
                this.waitingList.splice(randomIndex, 1);
            }
        }
    }

}
</script>

<style scoped lang="less">
.team-container {

    display: flex;
    flex-wrap: nowrap;
    height: 50vh;

    .team {
        width: 50%;
        padding: 10px;

        .team-name {
            text-align: center;
            font-size: 20px;
            font-weight: 700;
        }

        .user-list {
            border: 1px solid #eee;
            padding: 10px;
            min-height: 100px;
        }
    }

}

.user {
    display: inline-block;
    font-size: 20px;
    font-weight: 700;
    border: 1px solid #eee;
    margin: 5px;
    padding: 10px;
    border-radius: 5px;

}
</style>