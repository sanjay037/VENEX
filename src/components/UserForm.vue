<template>
    <v-tabs :value="tab" @change="onTabChange" grow>
        <v-tab>
            Residential
        </v-tab>
        <v-tab>
            Visitor
        </v-tab>
        <v-tab>
            Commercial
        </v-tab>
        <v-tab-item>
            <v-form ref="resform" v-model="resvalid">
                <v-text-field
                    v-model="vehicleNo"
                    label="Vehicle Number*"
                    :rules="vehicleRules"
                    requires
                ></v-text-field>
                <small>*indicates required field</small>
            </v-form>
        </v-tab-item>
        <v-tab-item>
            <v-form ref="vistform" v-model="vistvalid"
                ><v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-text-field
                                v-model="vehicleNo"
                                label="Vehicle Number*"
                                :rules="vehicleRules"
                                requires
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                v-model="firstname"
                                label="Legal first name*"
                                :rules="nameRules"
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                v-model="middlename"
                                label="Legal middle name"
                                hint="Middle name Optional"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                v-model="lastname"
                                label="Legal last name*"
                                :rules="nameRules"
                                hint="*Required"
                                persistent-hint
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                v-model="email"
                                label="Email"
                                :rules="emailRules"
                                hint="Email is Optional"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="phonenumber"
                                label="Phone Number*"
                                :rules="phoneRules"
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="flatno"
                                label="Flat Number*"
                                hint="whom they are visiting"
                                persistent-hint
                                :rules="flatRules"
                                required
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-container>
                <small>*indicates required field</small></v-form
            >
        </v-tab-item>
        <v-tab-item>
            <v-form ref="comform" v-model="comvalid"
                ><v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-text-field
                                v-model="vehicleNo"
                                label="Vehicle Number*"
                                :rules="vehicleRules"
                                requires
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="firstname"
                                label="Legal Name*"
                                :rules="nameRules"
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="companyname"
                                label="Company Name*"
                                hint="*Required"
                                :rules="compnameRules"
                                persistent-hint
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                v-model="email"
                                label="Email"
                                :rules="emailRules"
                                hint="Email is Optional"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="phonenumber"
                                label="Phone Number*"
                                :rules="phoneRules"
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="flatno"
                                label="Flat Number*"
                                hint="For Delivery"
                                :rules="flatRules"
                                persistent-hint
                                required
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-container>
                <small>*indicates required field</small></v-form
            >
        </v-tab-item>
    </v-tabs>
</template>

<script>
export default {
    props: { vistform: String, comform: String },
    data: () => ({
        tab: '',
        vistvalid: true,
        comvalid: true,
        resvalid: true,
        // action: 'Entry',
        vehicleNo: '',
        firstname: '',
        middlename: '',
        lastname: '',
        companyname: '',
        vehicleRules: [v => !!v || 'Vehicle Number is required'],
        compnameRules: [v => !!v || 'Company Name is required'],
        nameRules: [
            v => !!v || 'Name is required',
            v => (v && v.length <= 30) || 'Name must be less than 30 characters'
        ],
        email: '',
        emailRules: [v => !v || /.+@.+\..+/.test(v) || 'E-mail must be valid'],
        phonenumber: '',
        phoneRules: [
            v => !!v || 'Phone Number is required',
            v =>
                Number.isInteger(Number(v)) ||
                'The value must be an integer number',
            v => v > 0 || 'The value must be greater than zero',
            v => v > 999999999 || 'The Number must be Ten digit Number'
        ],
        flatno: '',
        flatRules: [v => !!v || 'Flat Number is required']
    }),
    methods: {
        async onTabChange(clickedTab) {
            this.tab = clickedTab;
        },
        validate() {
            if (this.tab == 0) this.$refs.resform.validate();
            else if (this.tab == 1) this.$refs.vistform.validate();
            else if (this.tab == 2) this.$refs.comform.validate();
        },
        reset() {
            if (this.tab == 0) this.$refs.resform.reset();
            else if (this.tab == 1) this.$refs.vistform.reset();
            else if (this.tab == 2) this.$refs.comform.reset();
        },
        resetValidation() {
            if (this.tab == 0) this.$refs.resform.resetValidation();
            else if (this.tab == 1) this.$refs.vistform.resetValidation();
            else if (this.tab == 2) this.$refs.comform.resetValidation();
        },
        valid() {
            if (this.tab == 0) this.resvalid;
            else if (this.tab == 1) return this.vistvalid;
            else if (this.tab == 2) return this.comvalid;
            else return false;
        }
    }
};
</script>
