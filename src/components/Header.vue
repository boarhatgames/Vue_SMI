<template>
  <!-- <v-card height="100%">
    <v-layout> -->
  <v-app-bar :elevation="4" rounded>
    <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
    <v-app-bar-title>SMI</v-app-bar-title>
  </v-app-bar>

  <v-navigation-drawer
    v-model="drawer"
    :rail="rail"
    permanent
    @click="rail = false"
  >
    <v-list-item
      :prependAvatar="user.defaultAvatar.thumbUrl"
      :title="user.firstName + ' ' + user.lastName"
      nav
    >
      <template v-slot:append>
        <v-btn
          variant="text"
          icon="mdi-chevron-left"
          @click.stop="rail = !rail"
        ></v-btn>
      </template>
    </v-list-item>

    <v-divider></v-divider>

    <v-list density="compact" nav>
      <v-list-item
        prepend-icon="mdi-account-group"
        title="Users"
        value="account"
      ></v-list-item>
      <v-list-group value="Items">
        <template v-slot:activator="{ props }">
          <v-list-item
            v-bind="props"
            prepend-icon="mdi-shape"
            title="Items"
            value="home"
          ></v-list-item>
        </template>
        <v-list-item title="Catalog" value="catalog" />
        <v-list-item to="s2w" title="Spin to Win" value="s2w" />
      </v-list-group>
      <v-list-item
        prepend-icon="mdi-home"
        title="Spaces"
        value="users"
      ></v-list-item>
      <v-list-item
        prepend-icon="mdi-hat-fedora"
        title="Missions"
        value="missions"
      ></v-list-item>
      <v-list-item
        prepend-icon="mdi-cogs"
        title="Administration"
        value="settings"
      ></v-list-item>
      <!-- <v-list-group value="Users">
        <template v-slot:activator="{ props }">
          <v-list-item
            v-bind="props"
            prepend-icon="mdi-account-circle"
            title="Users"
          ></v-list-item>
        </template>
        <v-list-item title="Admin" />
      </v-list-group> -->
    </v-list>
  </v-navigation-drawer>
  <!-- <v-main style="height: 100vh"></v-main>
    </v-layout>
  </v-card> -->
</template>

<script>
export default {
  name: 'Header',

  data() {
    return {
      user: {
        id: '4',
        firstName: 'random',
        lastName: 'random',
        email: 'rando@rando.com',
        goldBalance: 15185284,
        tokensBalance: 111868,
        sex: 'F',
        citizenLevel: 240,
        contentPath: 'https://content.smallworlds.app',
        citizenTitle: 'Citizen',
        citizenImageExt: 'Citizen',
        defaultAvatar: {
          id: 'tgirjpvnupcqzxgpkkuzsvmmifjjxbud',
          name: 'madisonsmallworlds',
          firstName: 'Madison',
          lastName: 'SmallWorlds',
          nameInstance: 1,
          fullName: 'Madison SmallWorlds',
          gender: 'female',
          takePet: true,
          header: true,
          citizenTitle: 'Commoner',
          ownerId: 'tgirjpvnupcqzxgpkkuzsvmmifjjxbud',
          pet: {
            status: true,
            snapUrl: 'https://avatars.smallworlds.app/LszQpPqVP6_snap.png',
          },
          avatarXPs: {
            artist: {
              level: 58,
              xp: 13600,
              levelXP: 13440,
            },
            explorer: {
              level: 499,
              xp: 225120,
              levelXP: 225120,
            },
            gamer: {
              level: 50,
              xp: 9600,
              levelXP: 9600,
            },
            social: {
              level: 499,
              xp: 225120,
              levelXP: 225120,
            },
            arena: {
              level: 50,
              xp: 9600,
              levelXP: 9600,
            },
            farmer: {
              level: 1,
              xp: 0,
              levelXP: 0,
            },
            crafter: {
              level: 200,
              xp: 158404,
              levelXP: 158404,
            },
            primary: {
              level: '205',
              xp: 641444,
              levelXP: 641350,
            },
          },
          dateCreated: '2021-07-05 20:33:52',
          thumbUrl:
            'https://avatars.smallworlds.app/tgirjpvnupcqzxgpkkuzsvmmifjjxbudVhUbcbmsxO_thumb.png',
          snapUrl:
            'https://avatars.smallworlds.app/tgirjpvnupcqzxgpkkuzsvmmifjjxbudVhUbcbmsxO_snap.png',
        },
        loyalty: {
          taskId: '2',
          progress: 3,
          progressPoints: 18,
          addEntry: true,
        },
        spaces: [
          {
            spaceId: 245,
            desc: 'Local Testing Zone',
          },
          {
            spaceId: 412,
            desc: "Madison's Entry Room",
          },
          {
            spaceId: 634,
            desc: "Madison's Variety Rooms",
          },
          {
            spaceId: 1001,
            desc: "Space's Test's House",
          },
          {
            spaceId: 1447,
            desc: 'Copy of Local Testing Zone',
          },
          {
            spaceId: 1686,
            desc: "Madison's Manor Hall",
          },
          {
            spaceId: 1687,
            desc: "Madison's Cosy Room",
          },
          {
            spaceId: 1688,
            desc: "Madison's Arid Plains",
          },
          {
            spaceId: 1689,
            desc: "Madison's Zoo",
          },
          {
            spaceId: 1784,
            desc: 'Worldview Condo',
          },
        ],
        permissions: [
          '1',
          '2',
          '3',
          '4',
          '5',
          '6',
          '7',
          '8',
          '9',
          '10',
          '11',
          '13',
          '14',
          '15',
          '16',
          '17',
          '18',
          '19',
          '20',
          '21',
          '22',
          '23',
          '24',
          '25',
          '26',
          '27',
          '28',
          '29',
          '31',
          '32',
          '33',
          '34',
          '35',
          '36',
          '38',
          '39',
          '40',
          '41',
          '42',
          '43',
          '44',
          '45',
          '46',
          '47',
          '48',
          '49',
          '51',
          '52',
          '53',
          '54',
          '55',
          '56',
          '57',
          '58',
          '59',
          '60',
          '61',
          '62',
          '63',
          '64',
          '65',
          '66',
          '67',
          '68',
          '69',
          '70',
          '71',
          '72',
          '73',
          '74',
          '75',
          '76',
          '77',
          '78',
          '81',
          '82',
          '84',
          '85',
          '86',
          '87',
          '88',
          '89',
          '90',
          '91',
          '92',
          '94',
          '95',
          '98',
          '99',
          '100',
          '101',
          '102',
          '103',
          '104',
          '105',
          '107',
          '108',
          '109',
          '110',
          '111',
          '112',
          '113',
          '114',
          '115',
          '117',
          '118',
          '119',
          '120',
          '121',
          '123',
          '124',
          '125',
          '126',
          '128',
          '129',
          '131',
          '132',
          '133',
          '136',
          '140',
          '141',
          '142',
          '143',
          '144',
          '145',
          '146',
          '150',
          '151',
          '153',
          '155',
          '158',
          '159',
          '160',
          '162',
          '163',
          '164',
          '165',
          '168',
          '169',
          '170',
          '171',
          '173',
          '174',
          '175',
          '176',
          '177',
          '178',
          '179',
          '180',
          '181',
          '182',
          '183',
          '184',
          '185',
          '186',
          '187',
          '188',
          '189',
          '190',
          '191',
          '192',
          '193',
          '194',
          '195',
          '196',
          '197',
          '198',
          '199',
          '200',
          '201',
          '202',
          '203',
          '204',
          '205',
          '206',
          '207',
          '208',
          '210',
          '211',
          '212',
          '213',
          '214',
          '215',
          '216',
          '217',
          '218',
          '219',
          '220',
          '221',
          '222',
          '223',
          '224',
          '225',
          '226',
          '227',
          '228',
          '229',
          '230',
          '231',
          '232',
          '233',
          '234',
          '235',
          '236',
          '237',
          '238',
          '239',
          '240',
          '241',
          '242',
          '116',
        ],
        activeAvatars: [
          'tgirjpvnupcqzxgpkkuzsvmmifjjxbud',
          '2xd1tzrs57mpl56ml6veixluhbwekag0',
          '74b0cpp7ec8yjatl3uqzzquo07ne0fvz',
          'dlo7xefql1nglt1qyj2ohh53c0df8138',
          'ffdoo4gdchwmxxpinidqaqdj4u3cs2pt',
          'or9b7n0ir5kjx2xpx9ofony6dc88fwvu',
          'wa6n8qzj22bepsxb6wlc336iuwzvvxun',
        ],
      },
      drawer: true,
      items: [
        { title: 'Home', icon: 'mdi-home-city' },
        { title: 'My Account', icon: 'mdi-account' },
        { title: 'Users', icon: 'mdi-account-group-outline' },
      ],
      rail: true,
    };
  },

  methods: {
    async getItems() {
      const response = await fetch('/api/items', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
      });
      const data = await response.json();
      return data;
    },

    toggleDrawer() {
      // v-navigation-drawer v-model="drawer"
      this.drawer = !this.drawer;
    },
    async fetchUserData() {
      const response = await fetch('http://localhost:3000/user', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
      });
      const data = await response.json();
      return data;
    },
  },

  watch: {
    group() {
      this.drawer = false;
    },
  },
  emits: ['update:group'],
};
</script>
